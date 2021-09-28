<script lang="ts">
  import { onMount } from "svelte";
  import Table from "svelte-table";
  import Field from "../Components/Field.svelte";
  import SelectInput from "../Components/SelectInput.svelte";
  import Input from "../Components/Input.svelte";
  import DateInput from "../Components/DateInput.svelte";
  import DeleteUser from "../Components/DeleteUser.svelte";
  import PieChart from "../Components/PieChart.svelte";

  let name = "";
  let lastname = "";
  let birthdate = "";
  let kind_document = "";
  let num_document = "";
  let vaccine = "";

  let options;
  const handleUser = () => {
    fetch("http://localhost:3000/user", {
      method: "POST",
      headers: {
        Accept: "application/json",
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        name,
        lastname,
        birthdate,
        kind_document,
        num_document,
        vaccine,
      }),
    }).then(async (res) => {
      const data = await res.json();
      !data?.error && (rows = [...rows, data]);
    });
  };

  let rows = [];
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
        // use first letter of _id to generate filter
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
      key: "name",
      title: "name",
      value: (v) => v.name,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of name to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.name.charAt(0);
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
      filterValue: (v) => v.name.charAt(0).toLowerCase(),
    },
    {
      key: "lastname",
      title: "lastname",
      value: (v) => v.lastname,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of lastname to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.lastname.charAt(0);
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
      filterValue: (v) => v.lastname.charAt(0).toLowerCase(),
    },
    {
      key: "birthdate",
      title: "birthdate",
      value: (v) => v.birthdate,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of birthdate to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.birthdate.charAt(0);
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
      filterValue: (v) => v.birthdate.charAt(0).toLowerCase(),
    },
    {
      key: "kind_document",
      title: "kind_document",
      value: (v) => v.kind_document,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of doc_vaccinator to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.kind_document.charAt(0);
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
      filterValue: (v) => v.kind_document.charAt(0).toLowerCase(),
    },
    {
      key: "num_document",
      title: "num_document",
      value: (v) => v.num_document,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of num_document to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.num_document.charAt(0);
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
      filterValue: (v) => v.num_document.charAt(0).toLowerCase(),
    },
    {
      key: "vaccine",
      title: "vaccine",
      value: (v) => v.vaccine,
      sortable: true,
      filterOptions: (rows) => {
        // use first letter of vaccine to generate filter
        let letrs = {};
        rows.forEach((row) => {
          let letr = row.vaccine.charAt(0);
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
      filterValue: (v) => v.vaccine.charAt(0).toLowerCase(),
    },
    {
      key: "_id2",
      title: "",
      value: (v) => v._id,
      // sortable: false,
      renderComponent: {
        component: DeleteUser,
        props: {
          actualizar,
        },
      },
    },
  ];
  let vaccines = [];
  let items = [];
  onMount(() => {
    fetch("http://localhost:3000/user").then(async (res) => {
      const data = await res.json();
      rows = [...data];
    });
    fetch("http://localhost:3000/vaccine").then(async (res) => {
      const data = await res.json();
      vaccines = [...data];
    });
  });
  const generateColor = () =>
    "#" + ((Math.random() * 0xffffff) << 0).toString(16).padStart(6, "0");
  const getData = () => {
    const dataMap = new Map<string, number>();
    for (const row of rows) {
      const id = row.vaccine.trim().toUpperCase();
      if (dataMap.has(id)) {
        dataMap.set(id, +dataMap.get(id) + 1);
      } else {
        dataMap.set(id, 1);
      }
    }
    return dataMap;
  };

  const handleSelect = (event) => {
    vaccine = event.detail.value;
  };
  const handleClear = () => {
    vaccine = undefined;
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
  $: if (vaccines) {
    items = vaccines.map((vaccine) => ({
      value: vaccine._id,
      label: vaccine.manufacturer,
    }));
  }
</script>

<div class="flex justify-center items-center flex-wrap">
  <form
    class="grid sm:grid-cols-2 grid-cols-1 sm:grid-rows-4 grid-flow-row gap-4"
    on:submit|preventDefault={handleUser}
  >
    <Field text={"Name"}>
      <Input id={"name"} bind:value={name} placeholder={"Ingrese algo..."} />
    </Field>
    <Field text={"Lastname"}>
      <Input
        id={"lastname"}
        bind:value={lastname}
        placeholder={"Ingrese algo..."}
      />
    </Field>
    <Field text={"Kind. Document"}>
      <Input
        id={"kind_document"}
        bind:value={kind_document}
        placeholder={"Ingrese algo..."}
      />
    </Field>
    <Field text={"Num. Document"}>
      <Input
        id={"num_document"}
        bind:value={num_document}
        placeholder={"Ingrese algo..."}
      />
    </Field>
    <Field text={"Birthdate"}>
      <DateInput id={"lot"} bind:value={birthdate} />
    </Field>
    <Field text={"Vaccine"}>
      <SelectInput id={"vaccine"} {items} {handleSelect} {handleClear} />
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
