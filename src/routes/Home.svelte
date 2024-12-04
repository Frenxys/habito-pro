<script>
    let habits = [
        { name: "Drink water", completed: false },
        { name: "Exercise", completed: false },
    ];
    let points = 0;

    function updatePoints() {
        points = habits.reduce((total, habit) => total + (habit.completed ? 10 : 0), 0);
    }
</script>

<main>
    <h1>Your Habits</h1>
    <p>Points: {points}</p>
    <ul>
        {#each habits as habit, index}
            <li>
                <input
                    type="checkbox"
                    bind:checked={habit.completed}
                    on:change={updatePoints}
                />
                {habit.name}
            </li>
        {/each}
    </ul>
</main>
