<script lang="ts">
  import { Grid,ContextMenu, type IApi, type IColumnConfig } from "@svar-ui/svelte-grid";
  import { Willow } from "@svar-ui/svelte-grid";

  import { m } from '$lib/paraglide/messages.js';
	import { setLocale } from "$lib/paraglide/runtime";

  const data = [{
    id: 1,
    quantity: 1,
    description: "Klieste",
    price: "34eur"
  },
  {
    id: 2,
    quantity: 2,
    description: "Monterky",
    price: "80eur"
  }]

  const columns: IColumnConfig[] = [
  {
    id: "quantity",
    header: m.quantity(),
    editor: "text",
    width: 110
  },
  {
    id: "description",
    header: m.description(),
    editor: "text",
    width: 300
  },
  {
    id: "unit_price",
    header: m.unit_price(),
    editor: "text",
    width: 110
  },
  {
    id: "vat_rate",
    header: m.vat_rate(),
    width: 110
  },
  {
    id: "vat_total",
    header: m.vat_total(),
    width: 110
  },
  {
    id: "price_total",
    header: m.price_total(),
    width: 110
  }]

  const init = (api: IApi) => {
    const cb = (ev: any) => {
      console.log(ev.value);
      return true // returning false prevents updating the cell
    }
    api.intercept("editor", cb);
  }

  let table: any = $state();

</script>

<div id="page" class="flex justify-center w-screen h-screen bg-gray-100">
	<button onclick={() => setLocale('en')}>🇺🇸</button>
	<button onclick={() => setLocale('sk')}>🇸🇰</button>

  <div id="paper" class="h-full w-full lg:w-1/2 p-6 rounded-2xl bg-white shadow-md">

      <div class="flex justify-center mt-6">
        <Willow>
          <ContextMenu api={table}>
            <Grid {data} {columns} {init} bind:this={table} multiselect/>
          </ContextMenu>
        </Willow>
      </div>

  </div>

</div>
