# Info Card

The InfoCard component has four variants: default, success, error and warning.

The default labels will be Info, Success, Error and Warning respectively for each variant.

But the label can be configurable using the label prop.

Also, we can send an array of elements that need to be shown in the info card component.

By default, the elements will be shown in the vertical direction and if you want to show them in the horizontal direction then the inline prop can be sent as true.

**With Additional Elements:**

```
<InfoCard
populators={{
name: "infocardwithelements",
}}
variant="default"
text={
"Application process will take a minute to complete. It might cost around Rs.500/- to Rs.1000/- to clean your septic tank and you can expect the service to get completed in 24 hrs from the time of payment."
}
label={"Info"}
additionalElements={[
<p key="1">Additional Element 1</p>,
<img
key="2"
src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"
alt="Additional Element 2"
/>,
<img
key="3"
src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"
alt="Additional Element 3"
/>,
<img
key="4"
src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"
alt="Additional Element 4"
/>,
<img
key="5"
src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"
alt="Additional Element 5"
/>,
<img
key="6"
src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"
alt="Additional Element 6"
/>,
<img
key="7"
src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIGMLufj86aep95KwMzr3U0QShg7oxdAG8gBPJ9ALIFQ&s"
alt="Additional Element 7"
/>,
<img
key="8"
src="https://digit.org/wp-content/uploads/2023/06/Digit-Logo-1.png"
alt="Additional Element 8"
/>,
]}
inline={true}
/>
```

For more information: [Storybook for infocard](https://unified-dev.digit.org/storybook/?path=/story/atom-groups-infocard--info)
