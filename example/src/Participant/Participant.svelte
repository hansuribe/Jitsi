<script>
  import { Video } from 'jitsi-svelte'

  export let participantId
  export let participant
</script>

<div class="container">
  <div class="left">
    <div>Local: {$participant.isLocal}</div>
    <div>Jitsi ID: {$participant.jid}</div>
    <div>Role: {$participant.role}</div>
    <div>Audio Level: {$participant.audioLevel}</div>
    <div>
      Audio:
      {#if $participant.audioEnabled}
        enabled
        <button
          on:click={() => participant.setAudioEnabled(false)}>mute</button>
      {:else}
        disabled
        <button
          on:click={() => participant.setAudioEnabled(true)}>unmute</button>
      {/if}
    </div>
    <div>
      Video:
      {#if $participant.videoEnabled}
        enabled
        <button
          on:click={() => participant.setVideoEnabled(false)}>mute</button>
      {:else}
        disabled
        <button
          on:click={() => participant.setVideoEnabled(true)}>unmute</button>
      {/if}
    </div>
    <div>Screen Enabled: {$participant.screenEnabled}</div>
    <div>Position: {JSON.stringify($participant.position)}</div>
    <div>Size: {$participant.size}</div>
    <div>Visible: {$participant.visible}</div>
  </div>
  <div class="right">
    {#if $participant.video}
      <div class="video">
        <Video track={$participant.video} mirror={$participant.isLocal} />
      </div>
    {/if}
  </div>
</div>

<style>
  .container {
    display: flex;
    flex-direction: row;

    margin-left: 2em;
    margin-bottom: 1em;
    border: 1px solid #ddd;

    width: 600px;
  }
  .left,
  .right {
    width: 50%;
  }
  .left {
    padding: 8px 15px;
  }
  .video {
    width: 300px;
    height: 300px;
    display: flex;
    object-fit: contain;
  }
</style>
