<script>
const germanStats = (async () => {
    const response = await fetch('https://api.corona-zahlen.org/germany')
    return await response.json()
})()

const globalStats = (async () => {
    const response = await fetch('https://api.covid19api.com/summary')
    return await response.json()
})()

const vaccinationsStats = (async () => {
    const response = await fetch('https://api.corona-zahlen.org/vaccinations')
    return await response.json()
})()

const incidenceStats = (async () => {
    const response = await fetch('https://api.corona-zahlen.org/germany/history/incidence/14')
    return await response.json()
})()

const options = {
    weekday: 'long',
    year: 'numeric',
    month: 'long',
    day: 'numeric'
};
</script>

<section class="m-5">
    <div class="container xl:max-w-4xl mx-auto">
        <p class="text-2xl font-semibold">🌎 Weltweite Statistik</p>

        {#await globalStats}
        <p>...waiting</p>
        {:then data}
        <div class="mt-4 grid gap-4 sm:grid-cols-1 md:grid-cols-3 lg:grid-cols-3 xl:grid-cols-3">
            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">Fälle</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.Global.TotalConfirmed.toLocaleString('de-DE')} <span class="opacity-30 font-medium text-sm rounded-md">+{data.Global.NewConfirmed.toLocaleString('de-DE')}</span></p>
                    </div>
                </div>
            </div>

            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">Genesen</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.Global.TotalRecovered.toLocaleString('de-DE')} <span class="opacity-30 font-medium text-sm rounded-md">+{data.Global.NewRecovered.toLocaleString('de-DE')}</span></p>
                    </div>
                </div>
            </div>

            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">Todesfälle</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.Global.TotalDeaths.toLocaleString('de-DE')} <span class="opacity-30 font-medium text-sm rounded-md">+{data.Global.NewDeaths.toLocaleString('de-DE')}</span></p>
                    </div>
                </div>
            </div>
        </div>
        <p class="mt-3 text-sm font-medium">Letzte Aktualisierung: {new Date(data.Date).toLocaleString('de-DE')}</p>
        {:catch error}
        <p>An error occurred!</p>
        {/await}
    </div>
</section>

<section class="m-5 mt-14">
    <div class="container xl:max-w-4xl mx-auto">
        <p class="text-2xl font-semibold">🇩🇪 Deutschland Statistik</p>

        {#await germanStats}
        <p>...waiting</p>
        {:then data}
        <div class="mt-4 grid gap-4 sm:grid-cols-1 md:grid-cols-3 lg:grid-cols-3 xl:grid-cols-3">
            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">Fälle</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.cases.toLocaleString('de-DE')}</p>
                    </div>
                </div>
            </div>

            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">Genesen</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.recovered.toLocaleString('de-DE')}</p>
                    </div>
                </div>
            </div>

            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">Todesfälle</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.deaths.toLocaleString('de-DE')}</p>
                    </div>
                </div>
            </div>
        </div>
        <p class="mt-3 text-sm font-medium">Letzte Aktualisierung: {new Date(data.meta.lastUpdate).toLocaleString('de-DE')}</p>
        <p class="mt-1 text-sm font-medium">7-Tage Inzidenz: {data.weekIncidence.toLocaleString('de-DE')}</p>
        {:catch error}
        <p>An error occurred!</p>
        {/await}
    </div>
</section>

<section class="m-5 mt-14">
    <div class="container xl:max-w-4xl mx-auto">
        <p class="text-2xl font-semibold">💉 Deutschland Impfstatistik</p>

        {#await vaccinationsStats}
        <p>...waiting</p>
        {:then data}
        <div class="mt-4 grid gap-4 sm:grid-cols-1 md:grid-cols-3 lg:grid-cols-3 xl:grid-cols-3">
            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">1. Impfung</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.data.vaccinated.toLocaleString('de-DE')}</p>
                    </div>
                </div>
            </div>

            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">2. Impfung</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.data.secondVaccination.vaccinated.toLocaleString('de-DE')}</p>
                    </div>
                </div>
            </div>

            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">3. Impfung</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.data.boosterVaccination.vaccinated.toLocaleString('de-DE')}</p>
                    </div>
                </div>
            </div>
        </div>
        <p class="mt-3 text-sm font-medium">Letzte Aktualisierung: {new Date(data.meta.lastUpdate).toLocaleString('de-DE')}</p>
        <p class="mt-1 text-sm font-medium">Komplett Geimpft: {data.data.administeredVaccinations.toLocaleString('de-DE')}</p>
        {:catch error}
        <p>An error occurred!</p>
        {/await}
    </div>
</section>

<section class="m-5 mt-14">
    <div class="container xl:max-w-4xl mx-auto">
        <p class="text-2xl font-semibold">📈 7-Tage Inzidenz</p>

        {#await incidenceStats}
        <p>...waiting</p>
        {:then data}
        <div class="mt-4 grid gap-4 sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-2 xl:grid-cols-2">
            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">Heute</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.data[13].weekIncidence.toLocaleString('de-DE')}</p>
                    </div>
                </div>
            </div>

            <div class="p-5 bg-gray-100 rounded shadow-sm">
                <div class="text-gray-600 font-medium">Heute vor einer Woche</div>
                <div class="flex items-center -mt-0.5">
                    <div class="text-lg text-white font-semibold">
                        <p class="mr-2 text-2xl text-black">{data.data[0].weekIncidence.toLocaleString('de-DE')}</p>
                    </div>
                </div>
            </div>
        </div>
        {:catch error}
        <p>An error occurred!</p>
        {/await}
    </div>
</section>
