<script>
  import { base } from "$app/paths"
  import SimpleLink from "$lib/components/SimpleLink.svelte"
  import SimpleCard from "$lib/components/SimpleCard.svelte"
  import IconBug from "$lib/components/Icons/IconBug.svelte"
  import Banner from "$lib/components/Banner.svelte"

  export let description = ""
  export let platform = ""
  export let browser = ""
  export let comments = ""

  $: disabled = description.length === 0
  $: criteria = disabled ? "text-colorError" : ""
</script>

<svelte:head>
  <title>Report a bug!</title>
  <meta name="description" content="Report a bug you found!" />
</svelte:head>

<!-- <div class="divider"></div> -->
<Banner />
<div class="mt-4 mx-auto sm:w-full max-w-lg flex flex-col gap-3">
  <h2
    class="mb-2 flex justify-center gap-2 text-xl fill-colorText font-semibold"
  >
    <IconBug /> Report a bug!
  </h2>
  <p class="text-center text-sm md:text-base text-colorTextSoft px-2 mb-2">
    Find a typo or broken link? Or does something just not work the way you
    expected? Whatever the bug is, describe it below!
  </p>
  <SimpleCard>
    <div class="flex justify-center items-center">
      <form
        class="w-full"
        method="POST"
        action="https://formspree.io/f/mbjnepbl"
      >
        <fieldset class="p-1 flex flex-col justify-end gap-2">
          <div class="formElementContainer">
            <label for="description"
              >Bug Description <span id="criteria" class={criteria}>
                (required)
              </span></label
            >
            <textarea
              bind:value={description}
              id="description"
              name="description"
              placeholder="describe the bug"
              rows="4"
              required
            />
          </div>
          <div class="formElementContainer">
            <label for="platform">Platform</label>
            <input
              bind:value={platform}
              type="text"
              id="platform"
              name="platform"
              placeholder="eg. Windows, iOS, Arch Linux, etc."
            />
          </div>
          <div class="formElementContainer">
            <label for="browser">Browser</label>
            <input
              bind:value={browser}
              type="text"
              id="browser"
              name="browser"
              placeholder="eg. Chrome, Firefox, Safari, etc."
            />
          </div>
          <div class="formElementContainer">
            <label for="comments">Comments</label>
            <textarea
              bind:value={comments}
              id="comments"
              name="comments"
              placeholder="share anything else here"
              rows="4"
            />
          </div>

          <button class="btn mt-2 mx-auto w-48" type="submit" {disabled}
            >Submit</button
          >
        </fieldset>
      </form>
    </div>
    <p class="text-center text-sm md:text-base">
      Form handling by <a href="https://formspree.io" target="_blank"
        >formspree.io</a
      >
    </p>
  </SimpleCard>
  <SimpleLink href="{base}/" text="Go back to collection" />
  <span class="text-center leading-none">or...</span>
  <SimpleLink href="{base}/suggest" text="Suggest a game!" />
</div>

<style lang="postcss">
  .formElementContainer {
    @apply flex flex-col justify-between;
    label {
      @apply font-semibold;
    }
  }
</style>
