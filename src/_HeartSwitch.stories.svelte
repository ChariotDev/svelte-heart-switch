<script>
  import { Meta, Template, Story } from "@storybook/addon-svelte-csf";
  import HeartSwitch from "./HeartSwitch.svelte";

</script>

<Meta
  title="HeartSwitch"
  component={HeartSwitch}
  argTypes={{
    // backgroundColor: { control: "color" },
    // label: { control: "text" },
    // onClick: { action: "onClick" },
    // primary: { control: "boolean" },
    size: {
      control: { type: 'select' },
      options: ['sm', 'md', 'lg'],
    },
  }}
/>

<Template let:args>
  <HeartSwitch {...args} />
</Template>

<Story
  name="Primary"
  args={{
    size: 'lg',
    onChange: () => console.log('Toggled')
  }}
/>

<Story
  name="Default"
  args={{
    onChange: () => console.log('Toggled'),
  }}
/>

<Story
  name="Checked"
  args={{
    onChange: () => console.log('Toggled'),
    checked: true,
  }}
/>

<Story
  name="Disabled"
  args={{
    onChange: () => console.log('Toggled'),
    disabled: true,
  }}
/>