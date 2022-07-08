<script>
  import Icon from "@iconify/svelte";

  const months = [
    "Jan",
    "Feb",
    "Mar",
    "Apr",
    "May",
    "Jun",
    "Jul",
    "Aug",
    "Sep",
    "Oct",
    "Nov",
    "Dec",
  ];

  const weekDays = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];

  let currentDate = new Date();
  let currentDay = currentDate.getDate();
  let currentMonth = currentDate.getMonth();
  let currentYear = currentDate.getFullYear();

  $: firsDayMonthIndex = new Date(currentYear, currentMonth).getDay();

  $: lastDayOfMonth = new Date(currentYear, currentMonth + 1, 0).getDate();

  function prevMonth() {
    if (currentMonth > 0) {
      currentMonth--;
    }
  }

  function nextMonth() {
    if (currentMonth < 11) {
      currentMonth++;
    }
  }
  $:console.log(firsDayMonthIndex)
</script>

<div class="calendar-container">
  <div class="calendar-header">
    <button on:click={prevMonth}
      ><Icon icon="ep:d-arrow-left" width="30" height="30" /></button
    >
    <div class="current-date">
      <p class="calendar-month">{months[currentMonth]}</p>
      <p class="calendar-date">{currentDate.toDateString()}</p>
    </div>
    <button on:click={nextMonth}
      ><Icon icon="ep:d-arrow-right" width="30" height="30" /></button
    >
  </div>
  <div class="calendar-body">
    <div class="calendar-week">
      {#each weekDays as days}
        <div>{days}</div>
      {/each}
    </div>
    <div class="calendar-days">
      {#each { length: firsDayMonthIndex } as _}
        <div />
      {/each}
      {#each { length: lastDayOfMonth } as _, i}
        <div
          class:current={i + 1 === currentDay &&
            currentMonth === new Date().getMonth()}
        >
          {i + 1}
        </div>
      {/each}
    </div>
  </div>
</div>

<style>
  .calendar-container {
    height: 100%;
    width: 100%;
  }
  .calendar-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 146px;
    background-color: #00bbf9;    
    padding: 10px 30px;
    min-width: 700px;
  }
  .current-date{
    text-align: center;
    color: #edf2f4;
  }
  .calendar-header > button {
    color: #edf2f4;
    background-color: #00bbf9;
    border: none;
    cursor: pointer;
    padding: 10px;
  }
  .calendar-month {
    font-size: 64px;
    font-weight: bold;
  }
  .calendar-date {
    font-size: 32px;
    margin-top: 10px;
  }
  .calendar-body {
    background-color: #2b2d42;
    min-width: 700px;
    min-height: 700px;
  }
  .calendar-week {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: repeat(1, 1fr);
    gap: 0;
  }
  .calendar-week > div {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 32px;
    color: #edf2f4;
    font-weight: bold;
    height: 100px;
  }
  .calendar-days {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: repeat(6, 1fr);
    grid-column-gap: 0px;
    grid-row-gap: 0px;
    height: calc(100vh - 246px);
  }
  .calendar-days > div {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 32px;
    color: #edf2f4;
    font-weight: bold;
    min-height: 100px;
    max-width: 100vw;
    min-width: 100px;
  }
  .calendar-days > div:hover {
    background-color: #464a6c;
    cursor: pointer;
  }
  .current {
    background-color: #00bbf9;
  }
</style>
