<script>
    import { onMount } from "svelte";
    let habits = [
        { name: "Drink water", completed: false, duration: "1 month", startDate: new Date() },
        { name: "Exercise", completed: false, duration: "1 week", startDate: new Date() },
    ];
    let points = 0;
    let newHabit = "";
    let newDuration = "1 month";

    // Toggle complete and update points
    function toggleComplete(index) {
        
        updatePoints();
    }

    // Add new habit
    function addHabit() {
        if (newHabit.trim() !== "") {
            habits = [...habits, { name: newHabit, completed: false, duration: newDuration, startDate: new Date() }];
            newHabit = "";
            newDuration = "1 month";  // Reset to default
            updatePoints();
        }
    }

    // Remove habit
    function removeHabit(index) {
        habits = habits.filter((_, i) => i !== index);
        updatePoints();
    }

    // Update points based on completed habits
    function updatePoints() {
        points = habits.reduce((total, habit) => total + (habit.completed ? 10 : 0), 0);
    }

    // Calculate the progress based on duration
    function getProgress(habit) {
        const today = new Date();
        const diffInDays = Math.floor((today - new Date(habit.startDate)) / (1000 * 3600 * 24));
        let totalDurationDays;

        if (habit.duration === "1 month") {
            totalDurationDays = 30;
        } else if (habit.duration === "1 week") {
            totalDurationDays = 7;
        } else if (habit.duration === "1 year") {
            totalDurationDays = 365;
        }

        return Math.min((diffInDays / totalDurationDays) * 100, 100); // Ensure it doesn't exceed 100%
    }
</script>

<main class="main-container">
    <div class="header">
        <h1>Your Habits</h1>
        <p class="points">Points: <span>{points}</span></p>
        <p>Completed: {habits.filter(habit => habit.completed).length} / {habits.length}</p>
    </div>

    <div class="habit-list">
        {#each habits as habit, index (habit.name)}
            <div class="habit-item" class:completed={habit.completed}>
                <input
                    type="checkbox"
                    bind:checked={habit.completed}
                    on:change={() => toggleComplete(index)}
                    id={"habit" + index}
                />
                <label for={"habit" + index}>{habit.name}</label>
                <div class="check-icon">
                    {#if habit.completed}
                        <i class="fas fa-check-circle"></i>
                    {/if}
                </div>
                <div class="progress-bar">
                    <div class="progress" style="width: {getProgress(habit)}%"></div>
                </div>
                <button class="remove-btn" on:click={() => removeHabit(index)}>Remove</button>
            </div>
        {/each}
    </div>

    <div class="add-habit">
        <input
            type="text"
            bind:value={newHabit}
            placeholder="Add a new habit"
        />
        <select bind:value={newDuration}>
            <option value="1 week">1 week</option>
            <option value="1 month">1 month</option>
            <option value="1 year">1 year</option>
        </select>
        <button on:click={addHabit}>Add Habit</button>
    </div>
</main>
<style>
    /* General styling */
    body {
        font-family: 'Arial', sans-serif;
        margin: 0;
        padding: 0;
        background-color: #121212;
        color: #e0e0e0;
    }

    .main-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 20px;
    }

    .header {
        background-color: #333;
        color: white;
        padding: 10px 20px;
        border-radius: 8px;
        text-align: center;
        margin-bottom: 20px;
        width: 100%;
    }

    .points span {
        font-weight: bold;
        font-size: 24px;
    }

    .habit-list {
        display: grid;
        grid-template-columns: 1fr;
        gap: 15px;
        width: 100%;
        max-width: 400px;
    }

    .habit-item {
        display: flex;
        align-items: center;
        justify-content: space-between;
        background-color: #333;
        padding: 15px;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        transition: transform 0.3s ease;
    }

    .habit-item.completed {
        background-color: #2e2e2e;
        transform: scale(1.05);
    }

    .habit-item input {
        transform: scale(1.5);
    }

    .habit-item label {
        flex-grow: 1;
        padding-left: 10px;
        font-size: 16px;
        color: #e0e0e0;
    }

    .check-icon {
        font-size: 20px;
        color: #76c7c0;
    }

    .habit-item.completed .check-icon {
        display: inline;
    }

    .habit-item .check-icon {
        display: none;
    }

    .habit-item .remove-btn {
        background: transparent;
        border: none;
        color: #e57373;
        cursor: pointer;
        font-size: 18px;
    }

    /* Hover effect for the habit item */
    .habit-item:hover {
        transform: translateY(-5px);
        box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
    }

    .add-habit {
        display: flex;
        align-items: center;
        margin-top: 20px;
    }

    .add-habit input {
        padding: 10px;
        border-radius: 8px;
        border: none;
        margin-right: 10px;
        width: 200px;
        background-color: #333;
        color: #e0e0e0;
    }

    .add-habit select {
        padding: 10px;
        border-radius: 8px;
        background-color: #333;
        color: #e0e0e0;
        margin-right: 10px;
    }

    .add-habit button {
        padding: 10px 15px;
        background-color: #76c7c0;
        border-radius: 8px;
        border: none;
        color: white;
        cursor: pointer;
    }

    .add-habit button:hover {
        background-color: #64b3b2;
    }

    .progress-bar {
        width: 100%;
        background-color: #555;
        border-radius: 5px;
        height: 10px;
        margin-top: 10px;
    }

    .progress {
        height: 100%;
        background-color: #76c7c0;
        border-radius: 5px;
        transition: width 0.3s ease;
    }
</style>
