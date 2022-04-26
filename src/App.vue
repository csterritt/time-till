<template>
  <div
    class="flex flex-row items-center min-h-16 md:mt-2 mb-4 md:mx-4 shadow-lg bg-secondary text-neutral-content md:rounded-box"
  >
    <div class="flex-1 px-2 mx-2">
      <span class="text-lg font-bold">Time until</span>
    </div>
  </div>

  <div class="card w-96 bg-base-200 shadow-xl mx-6 w-fit">
    <div class="card-body">
      <h2 class="card-title">Time until August 24, 2022:</h2>
      <p>About {{ days }}.</p>
    </div>
  </div>
</template>

<script setup>
const then = new Date()
then.setFullYear(2022)
then.setMonth(7)
then.setDate(24)
then.setHours(13)
const now = new Date()
let days = `Now in the past!`
if (now.getMonth() < 7 || (now.getMonth() === 7 && now.getDate() <= 23)) {
  let e = new Date(then)
  let b = new Date(now)
  let bMonth = b.getMonth()
  let bYear = b.getFullYear()
  let eYear = e.getFullYear()
  let eMonth = e.getMonth()
  let bDay = b.getDate()
  let eDay = e.getDate() + 1

  let eDays = 0
  if (
    eMonth === 0 ||
    eMonth === 2 ||
    eMonth === 4 ||
    eMonth === 6 ||
    eMonth === 7 ||
    eMonth === 9 ||
    eMonth === 11
  ) {
    eDays = 31
  }

  if (eMonth === 3 || eMonth === 5 || eMonth === 8 || eMonth === 10) {
    eDays = 30
  }

  if (
    (eMonth === 1 && eYear % 4 === 0 && eYear % 100 !== 0) ||
    eYear % 400 === 0
  ) {
    eDays = 29
  }

  if (eMonth === 1 && (eYear % 4 !== 0 || eYear % 100 === 0)) {
    eDays = 28
  }

  let bDays = 0
  if (
    bMonth === 0 ||
    bMonth === 2 ||
    bMonth === 4 ||
    bMonth === 6 ||
    bMonth === 7 ||
    bMonth === 9 ||
    bMonth === 11
  ) {
    bDays = 31
  }

  if (bMonth === 3 || bMonth === 5 || bMonth === 8 || bMonth === 10) {
    bDays = 30
  }

  if (
    (bMonth === 1 && bYear % 4 === 0 && bYear % 100 !== 0) ||
    bYear % 400 === 0
  ) {
    bDays = 29
  }

  if (bMonth === 1 && (bYear % 4 !== 0 || bYear % 100 === 0)) {
    bDays = 28
  }

  let FirstMonthDiff = bDays - bDay + 1

  if (eDay - bDay < 0) {
    eMonth = eMonth - 1
    eDay = eDay + eDays
  }

  let daysDiff = eDay - bDay

  if (eMonth - bMonth < 0) {
    eYear = eYear - 1
    eMonth = eMonth + 12
  }

  let monthDiff = eMonth - bMonth

  let yearDiff = eYear - bYear

  if (daysDiff === eDays) {
    daysDiff = 0
    monthDiff = monthDiff + 1

    if (monthDiff === 12) {
      monthDiff = 0
      yearDiff = yearDiff + 1
    }
  }

  if (FirstMonthDiff !== bDays && eDay - 1 === eDays) {
    daysDiff = FirstMonthDiff
  }
  days =
    monthDiff +
    ' month' +
    (monthDiff === 1 ? ', ' : 's, ') +
    daysDiff +
    ' day' +
    (daysDiff === 1 ? '' : 's')
}
</script>
