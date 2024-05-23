<template>
    <!-- Container für die Wettervorhersage der kommenden Tage -->
    <div class="days-tab text-center">
        <!-- Ladeanzeige -->
        <div class="loading">Lädt...</div>
        <!-- Liste für die Wettervorhersage der kommenden Tage -->
        <ul class="p-0">
            <!-- Eintrag für jeden Tag -->
            <li class="li_active">
                <!-- Wettericon -->
                <div class="py-3">icon</div>
                <!-- Wochentag -->
                <div class="py-3">day</div>
                <!-- Temperatur -->
                <div class="py-3">12oc</div>
            </li>
            <li class="li_active">
                <!-- Wettericon -->
                <div class="py-3">icon</div>
                <!-- Wochentag -->
                <div class="py-3">day</div>
                <!-- Temperatur -->
                <div class="py-3">12oc</div>
            </li>
            <li class="li_active">
                <!-- Wettericon -->
                <div class="py-3">icon</div>
                <!-- Wochentag -->
                <div class="py-3">day</div>
                <!-- Temperatur -->
                <div class="py-3">12oc</div>
            </li>
            <li class="li_active">
                <!-- Wettericon -->
                <div class="py-3">icon</div>
                <!-- Wochentag -->
                <div class="py-3">day</div>
                <!-- Temperatur -->
                <div class="py-3">12oc</div>
            </li>
        </ul>
    </div>
</template>

<script>
// Vue-Komponente definieren
export default (await import('vue')).defineComponent({
    // Name der Vue-Komponente
    name: 'App',
})
</script>

<style>
/* Stil für die Wettervorhersage der kommenden Tage */
.days-tab {
    width: 90%;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
    border-radius: 20px;
    width: 90%;
    margin: auto;
}

/* Stil für die Ladeanzeige */
.loading {
    color: #fff;
}

/* Stil für die Liste */
ul {
    margin: 0;
}

/* Stil für jeden Eintrag */
li {
    display: inline-block;
    list-style: none;
    height: 100%;
    width: 21%;
    max-width: 21%;
    font-size: 1vw;
    line-height: 1.2;
}

/* Stil für Text innerhalb eines Eintrags */
span {
    display: block;
    margin-bottom: 5px;
    font: 100% sans-serif;
    height: 35px;
}

/* Stil für aktive Einträge */
.li_active {
    background: #344457;
    color: #222831;
    border-radius: 10px;
    margin: 0.5rem;
    color: #fff;
    font-weight: 600;
}

/* Hover-Effekt für aktive Einträge */
.li_active:hover {
    transform: scale(1.2);
    transition: transform 0.1s ease-in-out;
}

/* Stil für die Temperaturanzeige in aktiven Einträgen */
.li_active_temp {
    display: inline-block;
    background-color: #222831;
    color: #fff;
    transition: background-color 0.5s;
    border-radius: 20px;
}

/* Hover-Effekt für die Temperaturanzeige in aktiven Einträgen */
.li_active_temp:hover {
    transform: scale(1.2);
    transition: transform 0.1s ease-in-out;
    background: #fff;
    border-radius: 20px;
    color: #191a1f
}
</style>
