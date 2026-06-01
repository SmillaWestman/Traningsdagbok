
<script>

    import {Dumbbell, Clock3, ChartColumn, Footprints, Bike, Waves, Plus, Trash2, Pencil, Timer, X} from "lucide-svelte";

    import{onMount} from "svelte"


    let showModal = $state(false);
    let editingWorkout = $state(null);

    let day =$state("Måndag")
    let training = $state("Löpning")
    let time = $state(30)
    let effort = $state("Medel")

    function closeModal() {
        showModal = false;
    }

    function saveWorkout() {
        if (editingWorkout) {
            workouts = workouts.map(w => 
                w.id === editingWorkout.id
                    ? { ...w, day, training, time, effort }
                    : w 
            );

            editingWorkout = null;
            
        } else {
            
            const workout = {
                id: crypto.randomUUID(),
                day,
                training,
                time: Number(time),
                effort
            }
            
            workouts = [...workouts, workout]

        }

            day = "Måndag"
            training = "Löpning"
            time = 30
            effort = "Medel"

            showModal = false;
    }

    let workouts = $state([])

    function getWorkoutsForDay(dayName) {
        return workouts.filter(w => w.day === dayName)
    }

    function deleteWorkout(id){
        workouts = workouts.filter(w => w.id !== id)
    }

    function totalWorkouts() {
        return workouts.length;
    }

    function totalMinutes() {
        return workouts.reduce((sum, w) => sum + Number(w.time), 0)
    }

    function intensitySummary() {
        const count = workouts.length;

        if (count === 0) return "Ingen träning ännu";
        if (count <= 3) return " 🟢 Låg belastning"
        if (count <=5) return " 🟡 Bra träningsvecka"

        return "🔴 Hög belastning"
    }

    function editWorkout(workout) {
        editingWorkout = workout;

        day = workout.day;
        training = workout.training;
        time = workout.time;
        effort = workout.effort;

        showModal = true;
    }

</script>

<h1 class="title">
    TRÄNINGS<span>DAGBOK</span>
</h1>
<p>FÅ KOLL PÅ DIN TRÄNING VECKA FÖR VECKA!</p>

<main class = "week" >

        <div class="row top">
            <section class="day"> 
                <h3>Måndag</h3>
            
                {#each getWorkoutsForDay("Måndag") as w}
                    <p class="workout-item">
                        
                        {#if w.training === "Löpning"}
                            <Footprints size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Cykel"}
                            <Bike size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Simning"}
                            <Waves size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Gym"}
                            <Dumbbell size={16} style="color: #00ff66;" />
                        {/if}
                        
                        {w.training} - {w.time} min ({w.effort})
                    </p>
                    <button class="icon-btn" onclick={() => deleteWorkout(w.id)}>
                        <Trash2 size={16} style="color: #00ff66;" />
                    </button>
                    <button class="icon-btn" onclick={() => editWorkout(w)}>
                        <Pencil size={16} style="color: #00ff66;" />
                    </button>
                {/each}   

            </section>
            <section class="day"> 
                <h3>Tisdag</h3>
            
                {#each getWorkoutsForDay("Tisdag") as w}
                    <p class="workout-item">
                        
                        {#if w.training === "Löpning"}
                            <Footprints size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Cykel"}
                            <Bike size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Simning"}
                            <Waves size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Gym"}
                            <Dumbbell size={16} style="color: #00ff66;" />
                        {/if}
                        
                        {w.training} - {w.time} min ({w.effort})
                    </p>
                    <button class="icon-btn" onclick={() => deleteWorkout(w.id)}>
                        <Trash2 size={16} style="color: #00ff66;" />
                    </button>
                    <button class="icon-btn" onclick={() => editWorkout(w)}>
                        <Pencil size={16} style="color: #00ff66;" />
                    </button>
                {/each}
            </section>
            <section class="day"> 
                <h3>Onsdag</h3>
            
                {#each getWorkoutsForDay("Onsdag") as w}
                    <p class="workout-item">
                        
                        {#if w.training === "Löpning"}
                            <Footprints size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Cykel"}
                            <Bike size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Simning"}
                            <Waves size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Gym"}
                            <Dumbbell size={16} style="color: #00ff66;" />
                        {/if}
                        
                        {w.training} - {w.time} min ({w.effort})
                    </p>
                    <button class="icon-btn" onclick={() => deleteWorkout(w.id)}>
                        <Trash2 size={16} style="color: #00ff66;" />
                    </button>
                    <button class="icon-btn" onclick={() => editWorkout(w)}>
                        <Pencil size={16} style="color: #00ff66;" />
                    </button>
                {/each}
            </section>
        </div>

        <div class="bottom row">
            <section class="day"> 
                <h3>Torsdag</h3>
            
                {#each getWorkoutsForDay("Torsdag") as w}
                    <p class="workout-item">
                        
                        {#if w.training === "Löpning"}
                            <Footprints size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Cykel"}
                            <Bike size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Simning"}
                            <Waves size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Gym"}
                            <Dumbbell size={16} style="color: #00ff66;" />
                        {/if}
                        
                        {w.training} - {w.time} min ({w.effort})
                    </p>
                    <button class="icon-btn" onclick={() => deleteWorkout(w.id)}>
                        <Trash2 size={16} style="color: #00ff66;" />
                    </button>
                    <button class="icon-btn" onclick={() => editWorkout(w)}>
                        <Pencil size={16} style="color: #00ff66;" />
                    </button>
                {/each}
            </section>
            <section class="day"> 
                <h3>Fredag</h3>
            
                {#each getWorkoutsForDay("Fredag") as w}
                    <p class="workout-item">
                        
                        {#if w.training === "Löpning"}
                            <Footprints size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Cykel"}
                            <Bike size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Simning"}
                            <Waves size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Gym"}
                            <Dumbbell size={16} style="color: #00ff66;" />
                        {/if}
                        
                        {w.training} - {w.time} min ({w.effort})
                    </p>
                    <button class="icon-btn" onclick={() => deleteWorkout(w.id)}>
                        <Trash2 size={16} style="color: #00ff66;" />
                    </button>
                    <button class="icon-btn" onclick={() => editWorkout(w)}>
                        <Pencil size={16} style="color: #00ff66;" />
                    </button>
                {/each}
            </section>
            <section class="day"> 
                <h3>Lördag</h3>
            
                {#each getWorkoutsForDay("Lördag") as w}
                    <p class="workout-item">
                        
                        {#if w.training === "Löpning"}
                            <Footprints size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Cykel"}
                            <Bike size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Simning"}
                            <Waves size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Gym"}
                            <Dumbbell size={16} style="color: #00ff66;" />
                        {/if}
                        
                        {w.training} - {w.time} min ({w.effort})
                    </p>
                    <button class="icon-btn" onclick={() => deleteWorkout(w.id)}>
                        <Trash2 size={16} style="color: #00ff66;" />
                    </button>
                    <button class="icon-btn" onclick={() => editWorkout(w)}>
                        <Pencil size={16} style="color: #00ff66;" />
                    </button>
                {/each}
            </section>
            <section class="day"> 
                <h3>Söndag</h3>
            
                {#each getWorkoutsForDay("Söndag") as w}
                    <p class="workout-item">
                        
                        {#if w.training === "Löpning"}
                            <Footprints size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Cykel"}
                            <Bike size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Simning"}
                            <Waves size={16} style="color: #00ff66;" />
                        {/if}

                        {#if w.training === "Gym"}
                            <Dumbbell size={16} style="color: #00ff66;" />
                        {/if}
                        
                        {w.training} - {w.time} min ({w.effort})
                    </p>
                    <button class="icon-btn" onclick={() => deleteWorkout(w.id)}>
                        <Trash2 size={16} style="color: #00ff66;" />
                    </button>
                    <button class="icon-btn" onclick={() => editWorkout(w)}>
                        <Pencil size={16} style="color: #00ff66;" />
                    </button>
                {/each}
            </section>
        </div>


    <button class = "knapp" onclick={() => showModal = true}> 
        + Lägg till pass
    </button>

    <div class="sammanställning">
        <h2>Veckosammanfattning</h2>

        <p>
            <Dumbbell size={18} style="color: #00ff66;" />
            Totala pass: {totalWorkouts()}
        </p>
        <p>
            <Clock3 size={18} style="color: #00ff66;" />
            Totala minuter: {totalMinutes()}
        </p>
        <p>
            <ChartColumn size={18} style="color: #00ff66;" />
            Veckobelastning: {intensitySummary()}
        </p>
    </div>

    {#if showModal}


    <div class="modal" >
        <div class ="modal-content" >

            <button
                class="close-btn"
                type="button"
                onclick={closeModal}
            >

                <X size={22} />
            </button>

            <h2> Nytt träningspass </h2>

            <label> Dag </label>
            <select bind:value={day}>
                <option>Måndag</option>
                <option>Tisdag</option>
                <option>Onsdag</option>
                <option>Torsdag</option>
                <option>Fredag</option>
                <option>Lördag</option>
                <option>Söndag</option>
            </select>

            <label> Typ av träning </label>
            <select bind:value={training}>
                <option>Löpning</option>
                <option>Gym</option>
                <option>Promenad</option>
                <option>Cykel</option>
                <option>Fotboll</option>
                <option>Innebandy</option>
                <option>Simning</option>
                <option>Annat</option>
            </select>

            <label> 
                <Timer size={16} />
                Tid 
            </label>
            <input type="number" bind:value={time}>

            <label> Ansträgning </label>
            <select bind:value={effort}>
                <option>Låg</option>
                <option>Medel</option>
                <option>Hög</option>
                <option>Mycket hög</option>
            </select>

            <button type="button" onclick={saveWorkout}>
                Spara
            </button>

        </div>
    </div>
    {/if}

</main>


<style>

    :global(body) {
        background: #474747;
        color: #fff;
        font-family: 'Montserrat', sans-serif;

    }

    .title {
        color: white;
        justify-self: center;
        font-size: 45px;
        font-weight: bold;
        letter-spacing: 1px;
    }

    .title span {
        color: #00ff66;
    }

    p {
        color: white;
        justify-self: center;
        font-weight: bold;
        font-size: 15px;
    }

    .week {
        display: flex;
        flex-direction: column;
        gap: 35px;
        margin-top: 70px;
        
    }

    .row.top {
        display: grid;
        grid-template-columns: repeat(3, 260px);
        justify-content: center;
        justify-content: center;
        
    }

    .bottom.row {
        display: grid;
        grid-template-columns: repeat(4, 260px);
        justify-content: center;
        justify-content: center;
    }

    .day {
        background-color: rgb(111, 111, 111);
        border-radius: 10px;
        border: 2px solid #00ff66;
        padding: 12px;
        min-height: 140px;
        height: auto;
        box-shadow: 0 6px 14px rgba(0, 0, 0, 0.06);
        width: 100%;
        max-width: 160px;

        font-weight: bold;
        
    }

    h2 {
        justify-self: center;

    }

    .sammanställning {
        background: rgba(111, 111, 111);
        padding: 15px;
        border-radius: 10px;
        border: 1px solid #00ff66;
        padding: 20px;
        box-shadow: 0 6px 14px rgba(0,0,0,0.1);
        width: 500px;
        align-self: center;

        box-shadow: 0 0 15px rgba(0,255,102,0.25);

        
    }

    .sammanställning h2 {
        color: #00ff66;
        font-size: 24px;
    }

    .sammanställning p {
        display: flex;
        align-items: center;
        gap: 10px;

    }

    .knapp {
        position: fixed;
        top: 180px;
        right: 200px;
        width: 150px;
        height: 50px;
        background-color: #00ff66;
        border: none;
        border-radius: 12px;
        color: rgb(0, 0, 0);
        cursor: pointer;
        font-weight: bold;
        box-shadow: 0 0 12px #00ff66;
    }

    .knapp:hover {
        background-color: rgb(166, 255, 194);
    }

    .modal {
        
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0,0,0,0.35);
        backdrop-filter: blur(6px);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal-content {
        position: relative;
        background: #2a2a2a;
        padding: 30px;
        border-radius: 16px;
        border: 1px solid #00ff66;
        width: 360px;
        box-shadow: 0 15px 35px rgba(0,0,0,0.15);

        display: flex;
        flex-direction: column;
        gap: 14px;
        animation: popup 0.25s ease; 
    }

    .close-btn {
        position: absolute;
        top: 10px;
        right: 10px;

        background: transparent;
        border: none;

        color: black;
        font-size: 22px;
        font-weight: bold;

        cursor: pointer;
        width: 40px;
        height: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
        }

    .close-btn:hover {
        color: #00ff66;
    }

    .modal-content label {
        font-weight: bold;
        margin-top: 5px;
    }

    .modal-content input, 
    .modal-content select {
        padding: 10px;
        border-radius: 10px;
        border: 1px solid #ccc;
        font-size: 15px;
    }

    .modal-content button {
        margin-top: 15px;
        padding: 12px;
        border: none;
        border-radius: 10px;
        background: #00ff66;
        cursor: pointer;
        font-weight: bold;
    }

    .modal-content button:hover {
        background: rgb(166, 255, 194);
    }

    @keyframes popup {
        from {
            opacity: 0;
            transform: scale(0.9) translateY(20px);
        }

        to {
            opacity: 1;
            transform: scale(1) translateY(0);
        }
    }

    

</style>