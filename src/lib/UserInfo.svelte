<!-- UserInfo.svelte -->
<script>
    import { onMount } from 'svelte';

    export let userName = 'Du Nguyen'; 
    export let startDate = new Date('2024-09-01'); 

    let currentDateTime = new Date();
    let daysSinceStart;
    let activeDays = 0; 

    onMount(() => {
        const interval = setInterval(() => {
            currentDateTime = new Date();
            calDaysStreak();
        }, 1000);
        return () => clearInterval(interval);
    });

    function calDaysStreak() {
        const now = new Date();
        const diffInTime = now - startDate;
        daysSinceStart = Math.floor(diffInTime / (1000 * 60 * 60 * 24)); 
    }

    calDaysStreak();
</script>

<main class="overview-container">
    <h2>Welcome to Aurum</h2>
    <div class="overview-details">
        <p><strong>Name:</strong> {userName}</p>
        <p><strong>Current Date/Time:</strong> {currentDateTime.toLocaleString()}</p>
        <p><strong>Days Since Beginning:</strong> {daysSinceStart} days</p>
        <p><strong>Active Days:</strong> {daysSinceStart} days</p>
    </div>
</main>

<style>
    .overview-container {
        background-color: #f9f9f9;
        padding: 1.5rem;
        border-radius: 10px;
        box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
        max-width: 600px;
        margin: 20px auto;
        background-color: #E6E6FA;
        border: 3px solid #A24C76;

    }

    .overview-details {
        font-size: 1.2rem;
        line-height: 1.6rem;
    }

    .overview-details p {
        margin: 10px 0;
    }

    h2 {
        margin-bottom: 1rem;
        color: #66023c;
    }

</style>