<script>
    let habits = ["Drink water", "Exercise", "Read a book"];
    let newHabit = "";

    function addHabit() {
        if (newHabit.trim()) {
            habits = [...habits, newHabit.trim()];
            newHabit = "";
        }
    }

    function removeHabit(index) {
        habits = habits.filter((_, i) => i !== index);
    }
</script>

<main>
    <h1>Your Habits</h1>
    <ul>
        {#each habits as habit, index}
            <li>
                {habit} <button on:click={() => removeHabit(index)}>Remove</button>
            </li>
        {/each}
    </ul>
    <input type="text" bind:value={newHabit} placeholder="New habit..." />
    <button on:click={addHabit}>Add Habit</button>
</main>
