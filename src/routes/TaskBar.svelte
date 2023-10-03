<script>
    import { windows } from './store.js';
    let id = 0;
  
    function openApp(title, body) {
      windows.update(n => [...n, { id: id++, content: { title, body } }]);
    }
  </script>
  
  <div class="taskbar">
    <button on:click={() => openApp('App 1', 'Content of App 1')}>App 1</button>
    <button on:click={() => openApp('App 2', 'Content of App 2')}>App 2</button>
  </div>
  
  <style>
    .taskbar {
      position: fixed;
      left: 0;
      bottom: 0;
      width: 100%;
      height: 30px;
      background-color: #333;
      color: white;
    }
  </style>
  