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
      options: ['small', 'medium', 'large'],
    },
  }}
/>

<Template let:args>
  <HeartSwitch {...args} />
</Template>

<Story
  name="Primary"
  args={{

  }}
/>