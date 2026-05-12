_Example file to illustrate structure and usage_

# Page layouts

## Standard page

A standard single-column page layout. Combines a `Heading level 2` with `xxlarge Stack` spacing between sections, where each section uses a `medium PageBlock` to establish content max width and consistent screen gutters.

```tsx
<Stack space="xxlarge">
  <PlaceholderHeader />

  <PageBlock width="medium">
    <Stack space="medium">
      <Heading level="2">Standard Page</Heading>

      <Text>
        Combines a <Strong>Heading level 2</Strong> with{" "}
        <Strong>xxlarge Stack</Strong> spacing between sections, where each
        section uses a <Strong>medium PageBlock</Strong> to establish content
        max width and consistent screen gutters.
      </Text>

      <Text>
        If providing text immediately below the Heading, consider using{" "}
        <Strong>standard Text</Strong> and grouping with a{" "}
        <Strong>medium Stack</Strong>.
      </Text>

      <Text>Use this layout as a starting point.</Text>
    </Stack>
  </PageBlock>

  <PageBlock width="medium">
    <Placeholder label="Section" height={300} />
  </PageBlock>

  <PageBlock width="medium">
    <Placeholder label="Section" height={250} />
  </PageBlock>

  <PageBlock width="medium">
    <Placeholder label="Section" height={400} />
  </PageBlock>
</Stack>
```
