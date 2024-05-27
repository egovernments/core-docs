# Configuring Gateway Rate Limiting

## Overview

Rate limiting in gateways is a crucial configuration to manage traffic and ensure service availability. By implementing a rate limiter, we can control the number of requests a client can make to the server within a specified time frame. This protects the underlying services from being overwhelmed by excessive traffic, whether malicious or accidental.&#x20;

The configuration typically involves -

1. **Replenish Rate**: The rate at which tokens are added to the bucket. For example, if the replenish rate is 2 tokens per second, two tokens are added to the bucket every second.
2. **Burst Capacity**: The maximum number of tokens that the bucket can hold. This allows for short bursts of traffic.
3. KeyResolver: A `KeyResolver` is an interface used to determine a key for rate-limiting purposes.

{% hint style="info" %}
**NOTE:** We currently provide two options for keyResolver and if none of them is specified the spring cloud will take a default go `PrincipalNameKeyResolver` which retrieves the `Principal` from the `ServerWebExchange` and calls `Principal.getName()`.

1. `ipKeyResolver :  Resolves key based on ip address of the request`
2. `userKeyResolver : Resolves key based on use UUID of the request`
{% endhint %}

## **Configuration Use Cases**

### **Example 1: Basic Rate Limiting**

Let's say we have a rate limiter configured with:

* `replenishRate`: 2 tokens per second
* `burstCapacity`: 5 tokens

This means:

* 2 tokens are added to the bucket every second.
* The bucket can hold a maximum of 5 tokens.

**Scenario**: A user makes requests at different intervals.

1. **Initial State**: The bucket has 5 tokens (full capacity).
2. **First Request**: The user makes a request and consumes 1 token. 4 tokens remain.
3. **Second Request**: The user makes another request and consumes 1 more token. 3 tokens remain.
4. **Third Request**: The user waits 1 second (2 tokens added) and then makes a request. The bucket has 4 tokens (3 remaining + 2 added - 1 consumed).

### **Example 2: Handling Burst Traffic**

Let's consider a scenario where a user makes multiple requests in quick succession.

**Configuration**:

* `replenishRate`: 1 token per second
* `burstCapacity`: 3 tokens

**Scenario**: A user makes 4 requests in rapid succession.

1. **Initial State**: The bucket has 3 tokens (full capacity).
2. **First Request**: Consumes 1 token. 2 tokens remain.
3. **Second Request**: Consumes 1 token. 1 token remains.
4. **Third Request**: Consumes 1 token. 0 tokens remain.
5. **Fourth Request**: There are no tokens left, so the request is denied. The user must wait for more tokens to be added.

After 1 second, 1 token is added to the bucket. The user can make another request.

### **Example 3: Applying Rate Limiting In Spring Cloud Gateway**

Here’s a practical example using Spring Cloud Gateway with Redis Rate Limiting.

**Configuration**: In Routes.properties you can set rate limiting as

```properties
spring.cloud.gateway.routes[5].id=egov-idgen
spring.cloud.gateway.routes[5].uri=http://egov-idgen.egov:8080/
spring.cloud.gateway.routes[5].predicates[0]=Path=/egov-idgen/**
spring.cloud.gateway.routes[5].filters[0].name=RequestRateLimiter
spring.cloud.gateway.routes[5].filters[0].args.redis-rate-limiter.replenishRate=5
spring.cloud.gateway.routes[5].filters[0].args.redis-rate-limiter.burstCapacity=10

```

**Explanation**:

* **Replenish Rate**: 5 tokens per second.
* **Burst Capacity**: 10 tokens.

**Behavior**:

* A user can make up to 10 requests instantly (burst capacity).
* After consuming the burst capacity, the user can make 5 requests per second (replenish rate).

### **Example 4: Real-World Use Case**

**API Service Rate Limiting**

An API service wants to ensure clients do not overwhelm the server with too many requests. They set up rate limits as follows:

* **Replenish Rate**: 100 tokens per minute.
* **Burst Capacity**: 200 tokens.

**Scenario**:

* A client can make 200 requests instantly.
* After the burst capacity is exhausted, the client can make 100 requests per minute.
* If any client tries to make more requests than allowed, they receive a response indicating they are being rate-limited.

## Rate Limiting - Benefits

1. **Prevents Abuse**: Limits the number of requests to prevent abuse or malicious attacks (e.g., DDoS attacks).
2. **Fair Usage**: Ensures fair usage among all users by preventing a single user from consuming all the resources.
3. **Load Management**: Helps manage server load and maintain performance by controlling the rate of incoming requests.
4. **Improved User Experience**: Prevents server overload, ensuring a smoother and more reliable experience for all users.

## Conclusion

Rate limiting is crucial for traffic management, fair usage, and server resource protection. By setting parameters like replenishRate and burstCapacity, you can regulate request flow and manage traffic spikes efficiently. In Spring Cloud Gateway, the Redis Rate Limiter filter offers a robust solution for implementing rate limiting on your routes.
