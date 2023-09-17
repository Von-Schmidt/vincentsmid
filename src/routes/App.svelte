<script>
    import './styles.css';
    import blob from '$lib/images/blob.png';
    import WindowManager from './WindowManager.svelte';
    import { writable } from 'svelte/store';
	import TaskBar from './TaskBar.svelte';

    export const windows = writable([]);
</script>

<main>
    <WindowManager {windows} />
    <TaskBar />
</main>

<style>
    main {
        position: relative;
        width: 100vw;
        height: 100vh;
    }
</style>