<script>
  export let communityName;

  import { getClient } from '@urql/svelte';

  // datasources
  import sessionsApi from '../../dataSources/api.that.tech/sessions';
  import currentEvent from '../../store/currentEvent';

  import UpNextHero from '../../components/activities/UpNextHero.svelte';

  const { querySessionsByDate } = sessionsApi(getClient());
</script>

<section>
  {#await querySessionsByDate($currentEvent.eventId)}
    <p>loading...</p>
  {:then activities}
    <UpNextHero activityName="{communityName}" />
  {:catch error}
    <p>OH NO</p>
  {/await}
</section>
