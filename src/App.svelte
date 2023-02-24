<script>
  import { onMount } from 'svelte';

  import { setAPIKey } from "luna-park";
  import { LpLogicEditor} from "luna-park";
  import { loadApplication } from "luna-park";

  import { LpConsolePanel } from "luna-park";
  import { LpInspectorPanel } from "luna-park";

  import { loadNodeLib } from "luna-park";
  import { LogicNodes as LogicNodesStandard } from "@luna-park/lib-standard";
  import { LogicNodes as LogicNodesString } from "@luna-park/lib-string";

  setAPIKey(import.meta.env.VITE_LUNA_PARK_API_KEY);

  const editorId = "lana-park-editor";

  loadApplication();

  const editor = new LpLogicEditor({ editorId, standalone: true });

  const consoleElement = new LpConsolePanel({
    editorId: editorId
  })

  const inspectorElement = new LpInspectorPanel({
    editorId: editorId
  })

  loadNodeLib(editorId, LogicNodesStandard);
  loadNodeLib(editorId, LogicNodesString);

  onMount(() => {
    document.querySelector("#editor").append(editor);
    document.querySelector("#console").append(consoleElement);
    document.querySelector("#inspector").append(inspectorElement);
  });
</script>

<main>
  <div id="editor"></div>
  <div id="console"></div>
  <div id="inspector"></div>
</main>

<style>
  main {
    display: grid;
    grid-template-areas: 
      "editor inspector"
      "console console";
    grid-template-columns: auto 200px;
    grid-template-rows: auto 200px;
    width: 100vw;
    height: 100vh;
  }

  #editor {
    grid-area: editor;
  }

  #console {
    grid-area: console;
    overflow: hidden;
  }

  #inspector {
    grid-area: inspector;
  }
</style>
