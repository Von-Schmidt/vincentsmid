<script>
    import './styles.css';
    import TaskBar from './TaskBar.svelte';
    import WindowManager from './WindowManager.svelte';
    import { writable } from 'svelte/store';

    export const windows = writable([]);
</script>

<section>
    <WindowManager />
    <TaskBar />
</section>

<style>
    section {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        flex: 0.4;
    }
</style>