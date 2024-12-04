<script>
    let habits = [
        { name: "Drink water", completed: false },
        { name: "Exercise", completed: false },
    ];
    let points = 0;

    function toggleComplete(index) {
        points = habits.reduce((total, habit) => total + (habit.completed ? 10 : 0), 0);
    }
</script>

<main>
    <div class="header">
        <h1>Your Habits</h1>
        <p class="points">Points: <span>{points}</span></p>
    </div>
    
    <div class="habit-list">
        {#each habits as habit, index}
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
            </div>
        {/each}
    </div>
</main>

<style>
    /* General styling */
    body {
        font-family: 'Arial', sans-serif;
        background-color: #f3f4f6;
        margin: 0;
        padding: 0;
    }

    main {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 20px;
    }

    .header {
        background-color: #4CAF50;
        color: white;
        padding: 10px 20px;
        border-radius: 8px;
        text-align: center;
        margin-bottom: 20px;
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
        background-color: white;
        padding: 15px;
        border-radius: 8px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        transition: transform 0.3s ease;
    }

    .habit-item.completed {
        background-color: #e0f7fa;
        transform: scale(1.05);
    }

    .habit-item input {
        transform: scale(1.5);
    }

    .habit-item label {
        flex-grow: 1;
        padding-left: 10px;
        font-size: 16px;
        color: #333;
    }

    .check-icon {
        font-size: 20px;
        color: #4CAF50;
    }

    .habit-item.completed .check-icon {
        display: inline;
    }

    .habit-item .check-icon {
        display: none;
    }

    /* Hover effect for the habit item */
    .habit-item:hover {
        transform: translateY(-5px);
        box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
    }
</style>


