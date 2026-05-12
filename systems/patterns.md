_Example file to illustrate structure and usage_

# Design patterns

## Divided list

A layout approach for related items that allows users to easily scan, locate, edit and take action. This example also includes bulk actions.

```tsx
<PageBlock width="medium">
  <Stack space="large">
    <Stack space="small">
      <Heading level="2">List heading</Heading>
      <Text tone="secondary">3 lorem ipusm</Text>
    </Stack>

    <Stack space="small">
      <Columns alignY="center">
        <Column>
          <Inline space="medium" alignY="center">
            <CheckboxStandalone
              aria-label="Select all"
              checked={[getState("one"), getState("two"), getState("three")]}
              onChange={({ currentTarget: { checked } }) => {
                setState("one", checked);
                setState("two", checked);
                setState("three", checked);
              }}
            />

            {(getState("one") || getState("two") || getState("three")) && (
              <Inline space="large">
                <ButtonIcon
                  bleed
                  icon={<IconDownload />}
                  label="Download selected"
                  onClick={() =>
                    showToast({
                      key: "1",
                      message: "Positive toast",
                      tone: "positive",
                    })
                  }
                />
                <ButtonIcon
                  bleed
                  icon={<IconDelete />}
                  label="Delete selected"
                  onClick={() => toggleState("dialog")}
                />
              </Inline>
            )}
          </Inline>
        </Column>
        <Column>
          <Inline align="right">
            <ButtonIcon
              bleed={responsiveValue({
                mobile: false,
                tablet: true,
              })}
              variant="soft"
              icon={<IconSort />}
              label="Sort"
              id="sort"
            />
          </Inline>
        </Column>
      </Columns>

      <Stack space="large">
        <Divider />

        <Columns space="small">
          <Column width="content">
            <Text>
              <CheckboxStandalone
                aria-label="one"
                checked={getState("one")}
                onChange={() => toggleState("one")}
              />
            </Text>
          </Column>
          <Column>
            <Stack space="small">
              <Text weight="strong">List item 1</Text>
              <Text tone="secondary">A line of secondary text</Text>
            </Stack>
          </Column>
          <Column width="content">
            <Inline space="medium">
              <ButtonIcon
                variant="transparent"
                icon={<IconDownload />}
                label="Download"
                id="buttonicon-transparent"
                onClick={() =>
                  showToast({
                    key: "3",
                    message: "Positive toast",
                    tone: "positive",
                  })
                }
              />
              <ButtonIcon
                variant="transparent"
                icon={<IconDelete />}
                label="Delete"
                id="buttonicon-transparent"
                onClick={() => toggleState("dialog")}
              />
            </Inline>
          </Column>
        </Columns>

        <Divider />

        <Columns space="small">
          <Column width="content">
            <Text>
              <CheckboxStandalone
                aria-label="two"
                checked={getState("two")}
                onChange={() => toggleState("two")}
              />
            </Text>
          </Column>
          <Column>
            <Stack space="small">
              <Text weight="strong">List item 2</Text>
              <Text tone="secondary">A line of secondary text</Text>
            </Stack>
          </Column>
          <Column width="content">
            <Inline space="medium">
              <ButtonIcon
                variant="transparent"
                icon={<IconDownload />}
                label="Download"
                id="buttonicon-transparent"
                onClick={() =>
                  showToast({
                    key: "4",
                    message: "Positive toast",
                    tone: "positive",
                  })
                }
              />
              <ButtonIcon
                variant="transparent"
                icon={<IconDelete />}
                label="Delete"
                id="buttonicon-transparent"
                onClick={() => toggleState("dialog")}
              />
            </Inline>
          </Column>
        </Columns>

        <Divider />

        <Columns space="small">
          <Column width="content">
            <Text>
              <CheckboxStandalone
                aria-label="three"
                checked={getState("three")}
                onChange={() => toggleState("three")}
              />
            </Text>
          </Column>
          <Column>
            <Stack space="small">
              <Text weight="strong">List item 3</Text>
              <Text tone="secondary">A line of secondary text</Text>
            </Stack>
          </Column>
          <Column width="content">
            <Inline space="medium">
              <ButtonIcon
                variant="transparent"
                icon={<IconDownload />}
                label="Download"
                id="buttonicon-transparent"
                onClick={() =>
                  showToast({
                    key: "5",
                    message: "Positive toast",
                    tone: "positive",
                  })
                }
              />
              <ButtonIcon
                variant="transparent"
                icon={<IconDelete />}
                label="Delete"
                id="buttonicon-transparent"
                onClick={() => toggleState("dialog")}
              />
            </Inline>
          </Column>
        </Columns>

        <Divider />
      </Stack>
    </Stack>
  </Stack>
</PageBlock>

<Dialog
  title="Dialog title"
  open={getState("dialog")}
  onClose={() => toggleState("dialog")}
>
  <Text>Lorem ipsum dolor sit amet consectetur adipiscing elit?</Text>
  <Actions>
    <Button
      onClick={() => (
        toggleState("dialog"),
        showToast({
          tone: "positive",
          message: "Positive toast",
        })
      )}
      variant="solid"
      tone="critical"
      icon={<IconDelete />}
    >
      Delete
    </Button>
    <Button variant="transparent" onClick={() => toggleState("dialog")}>
      Cancel
    </Button>
  </Actions>
</Dialog>
```

---

## Empty state

A message shown when there is no data available at the present time.

```tsx
<PageBlock>
  <Box background="surface" borderRadius="large" padding="gutter">
    <ContentBlock width="small">
      <Stack align="center" space={{ mobile: "medium", desktop: "large" }}>
        <Placeholder
          shape="round"
          width={responsiveValue({
            mobile: "96px",
            tablet: "128px",
            desktop: "192px",
          })}
          height={responsiveValue({
            mobile: "96px",
            tablet: "128px",
            desktop: "192px",
          })}
        />

        <Stack space="medium" align="center">
          <Heading level="2" weight="weak" align="center">
            An example empty state
          </Heading>
          <Text tone="secondary" align="center">
            This is a center aligned example with a short summary. You can use a
            button or <TextLink href="#">a TextLink</TextLink> to suit your
            needs.
          </Text>

          <Actions>
            <Button variant="ghost">Button</Button>
          </Actions>
        </Stack>
      </Stack>
    </ContentBlock>
  </Box>
</PageBlock>
```

---

## Nudge

A prominent message that encourages the user to take a specific action.

```tsx
<Box background="formAccentSoft" padding="gutter" borderRadius="large">
  <Columns reverse space="gutter" collapseBelow="tablet">
    <Column width="content">
      <Columns space="xsmall">
        <Column>
          <Box
            background="surface"
            borderRadius="full"
            padding={{ mobile: "small", tablet: "medium" }}
            display="inlineBlock"
          >
            <Placeholder
              shape="round"
              label="illo"
              width={responsiveValue({
                mobile: "80px",
                tablet: "96px",
              })}
              height={responsiveValue({
                mobile: "80px",
                tablet: "96px",
              })}
            />
          </Box>
        </Column>
        <Column width="content">
          <ButtonIcon
            variant="transparent"
            icon={<IconClear />}
            label="Close"
            bleed
          />
        </Column>
      </Columns>
    </Column>
    <Column>
      <Stack space="medium">
        <Heading level="4">Create a nudge today</Heading>
        <Text>
          Use a nudge to drive specific behaviour that leads to better outcomes
          for customers or SEEK.
        </Text>
        <Inline>
          <Button>Create nudge</Button>
        </Inline>
      </Stack>
    </Column>
  </Columns>
</Box>
```

---
