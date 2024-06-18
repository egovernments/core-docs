# Info Card

## Description

The InfoCard component has four variants: default, success, error and warning. The default labels for these variants are Info, Success, Error and Warning.

However, the label can be configured using the label prop. The configuration enables users to set the array of elements for display in the info card component.

By default, the elements are shown in the vertical direction. To show the elements in the horizontal direction set the inline prop to true.

## Configuration

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
