<script lang="ts">
  import { onMount } from "svelte";
  import Table from "svelte-table";
  import Field from "../Components/Field.svelte";
  import Input from "../Components/Input.svelte";
  import DateInput from "../Components/DateInput.svelte";
  import DeleteVaccine from "../Components/DeleteVaccine.svelte";
  import PieChart from "../Components/PieChart.svelte";

  let manufacturer = "";
  let date = "";
  let doc_vaccinator = "";
  let name_vaccinator = "";
  let ips = "";
  let lot = "";

  let options;
  const handleVaccine = () => {
    fetch("http://localhost:3000/vaccine", {
      method: "POST",
      headers: {
        Accept: "application/json",
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        manufacturer,
        date,
        doc_vaccinator,
        name_vaccinator,
        ips,
        lot,
      }),
    }).then(async (res) => {
      const data = await res.json();
      !data?.error && (rows = [...rows, data]);
    });
  };

  let rows = [];

  onMount(() => {
    fetch("http://localhost:3000/vaccine").then(async (res) => {
      const data = await res.json();
      rows = [...data];
    });
  });
  const actualizar = (_id) => {
    rows = rows.filter((row) => row._id !== _id);
  };
  const columns = [
    {
      key: "_id",
      title: "ID",
      value: (v) => v._id,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of manufacturer to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row._id.charAt(0);
          if (letrs[letr] === undefined)
            letrs[letr] = {
              name: `${letr.toUpperCase()}`,
              value: letr.toLowerCase(),
            };
        });
        // fix order
        letrs = Object.entries(letrs)
          .sort()
          .reduce((o, [k, v]) => ((o[k] = v), o), {});
        return Object.values(letrs);
      },
      filterValue: (v) => v._id.charAt(0).toLowerCase(),
      headerClass: "text-left",
    },
    {
      key: "manufacturer",
      title: "manufacturer",
      value: (v) => v.manufacturer,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of manufacturer to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.manufacturer.charAt(0);
          if (letrs[letr] === undefined)
            letrs[letr] = {
              name: `${letr.toUpperCase()}`,
              value: letr.toLowerCase(),
            };
        });
        // fix order
        letrs = Object.entries(letrs)
          .sort()
          .reduce((o, [k, v]) => ((o[k] = v), o), {});
        return Object.values(letrs);
      },
      filterValue: (v) => v.manufacturer.charAt(0).toLowerCase(),
    },
    {
      key: "date",
      title: "date",
      value: (v) => v.date,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of date to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.date.charAt(0);
          if (letrs[letr] === undefined)
            letrs[letr] = {
              name: `${letr.toUpperCase()}`,
              value: letr.toLowerCase(),
            };
        });
        // fix order
        letrs = Object.entries(letrs)
          .sort()
          .reduce((o, [k, v]) => ((o[k] = v), o), {});
        return Object.values(letrs);
      },
      filterValue: (v) => v.date.charAt(0).toLowerCase(),
    },
    {
      key: "doc_vaccinator",
      title: "doc_vaccinator",
      value: (v) => v.doc_vaccinator,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of doc_vaccinator to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.doc_vaccinator.charAt(0);
          if (letrs[letr] === undefined)
            letrs[letr] = {
              name: `${letr.toUpperCase()}`,
              value: letr.toLowerCase(),
            };
        });
        // fix order
        letrs = Object.entries(letrs)
          .sort()
          .reduce((o, [k, v]) => ((o[k] = v), o), {});
        return Object.values(letrs);
      },
      filterValue: (v) => v.doc_vaccinator.charAt(0).toLowerCase(),
    },
    {
      key: "name_vaccinator",
      title: "name_vaccinator",
      value: (v) => v.name_vaccinator,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of doc_vaccinator to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.name_vaccinator.charAt(0);
          if (letrs[letr] === undefined)
            letrs[letr] = {
              name: `${letr.toUpperCase()}`,
              value: letr.toLowerCase(),
            };
        });
        // fix order
        letrs = Object.entries(letrs)
          .sort()
          .reduce((o, [k, v]) => ((o[k] = v), o), {});
        return Object.values(letrs);
      },
      filterValue: (v) => v.name_vaccinator.charAt(0).toLowerCase(),
    },
    {
      key: "ips",
      title: "ips",
      value: (v) => v.ips,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of ips to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.ips.charAt(0);
          if (letrs[letr] === undefined)
            letrs[letr] = {
              name: `${letr.toUpperCase()}`,
              value: letr.toLowerCase(),
            };
        });
        // fix order
        letrs = Object.entries(letrs)
          .sort()
          .reduce((o, [k, v]) => ((o[k] = v), o), {});
        return Object.values(letrs);
      },
      filterValue: (v) => v.ips.charAt(0).toLowerCase(),
    },
    {
      key: "lot",
      title: "lot",
      value: (v) => v.lot,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of lot to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.lot.charAt(0);
          if (letrs[letr] === undefined)
            letrs[letr] = {
              name: `${letr.toUpperCase()}`,
              value: letr.toLowerCase(),
            };
        });
        // fix order
        letrs = Object.entries(letrs)
          .sort()
          .reduce((o, [k, v]) => ((o[k] = v), o), {});
        return Object.values(letrs);
      },
      filterValue: (v) => v.lot.charAt(0).toLowerCase(),
    },
    {
      key: "_id2",
      title: "",
      value: (v) => v._id,
      // sortable: false,
      renderComponent: {
        component: DeleteVaccine,
        props: {
          actualizar,
        },
      },
    },
  ];
  const generateColor = () =>
    "#" + ((Math.random() * 0xffffff) << 0).toString(16).padStart(6, "0");
  const getData = () => {
    const dataMap = new Map<string, number>();
    for (const row of rows) {
      const id = row.ips.trim().toUpperCase();
      if (dataMap.has(id)) {
        dataMap.set(id, +dataMap.get(id) + 1);
      } else {
        dataMap.set(id, 1);
      }
    }
    return dataMap;
  };
  $: if (rows) {
    const generated_data = getData();
    const labels = Array.from(generated_data.keys());
    const data = Array.from(generated_data.values());
    console.log({ labels, data });
    options = {
      type: "doughnut",
      data: {
        labels,
        datasets: [
          {
            data,
            backgroundColor: labels.map((l) => generateColor()),
          },
        ],
      },
    };
  }
</script>

<div class="flex justify-center items-center flex-wrap">
  <form
    class="grid sm:grid-cols-2 grid-cols-1 sm:grid-rows-4 grid-flow-row gap-4"
    on:submit|preventDefault={handleVaccine}
  >
    <Field text={"Manufacturer"}>
      <Input
        id={"manufacturer"}
        bind:value={manufacturer}
        placeholder={"Ingrese algo..."}
      />
    </Field>
    <Field text={"Date"}>
      <DateInput id={"date"} bind:value={date} />
    </Field>
    <Field text={"Doc. Vaccinator"}>
      <Input
        id={"doc_vaccinator"}
        bind:value={doc_vaccinator}
        placeholder={"Ingrese algo..."}
      />
    </Field>
    <Field text={"Name. Vaccinator"}>
      <Input
        id={"name_vaccinator"}
        bind:value={name_vaccinator}
        placeholder={"Ingrese algo..."}
      />
    </Field>
    <Field text={"IPS"}>
      <Input id={"ips"} bind:value={ips} placeholder={"Ingrese algo..."} />
    </Field>
    <Field text={"lot"}>
      <Input id={"lot"} bind:value={lot} placeholder={"Ingrese algo..."} />
    </Field>
    <button
      class="h-8 flex justify-center items-center text-white bg-red-600 rounded-full hover:bg-red-700 active:shadow-lg mouse shadow transition ease-in duration-200 focus:outline-none"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-6 w-6"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M5 13l4 4L19 7"
        />
      </svg>
      <span>Submit</span>
    </button>
  </form>
  <PieChart clss={"object-cover h-1"} {options} />
  <Table {columns} {rows} />
  {#if !rows.length}
    No hay datos
  {/if}
</div>
