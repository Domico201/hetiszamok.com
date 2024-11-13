const spinButton = document.getElementById('spinButton');
const wheel = document.getElementById('wheel');
const resultDisplay = document.getElementById('result');

// Generáljuk le a szegmenseket
for (let i = 0; i < 25; i++) {
    const segment = document.createElement('div');
    segment.className = 'segment';
    segment.style.transform = `rotate(${(i * 360) / 25}deg)`;
    segment.innerText = i + 1; // Szegmensek számának megjelenítése
    wheel.appendChild(segment);
}

spinButton.addEventListener('click', () => {
    const randomDegree = Math.floor(Math.random() * 360 + 3600); // 10 teljes pörgetés + véletlenszerű fok
    wheel.style.transform = `rotate(${randomDegree}deg)`;

    // Várjunk, amíg a kerék megáll, majd számoljuk ki a pörgetett számot
    setTimeout(() => {
        const actualDegree = randomDegree % 360; // Az aktuális fok
        const segmentAngle = 360 / 25; // Mivel 25 szegmens van
        const segmentIndex = Math.floor((actualDegree + segmentAngle / 2) / segmentAngle); // Középpont alapján számoljuk
        resultDisplay.innerText = `Pörgetett szám: ${segmentIndex + 1}`;
    }, 4000); // 4 másodperc a pörgetés időtartama
});
