document.addEventListener("DOMContentLoaded", () => {

    const tabs = document.querySelectorAll(".tab");
    const cards = document.querySelectorAll(".media-card");
    const empty = document.getElementById("empty-message");

    if (!tabs.length || !cards.length) return;

    tabs.forEach(tab => {

        tab.addEventListener("click", () => {

            // Update active tab
            tabs.forEach(item => {
                item.classList.remove("active");
                item.setAttribute("aria-pressed", "false");
            });

            tab.classList.add("active");
            tab.setAttribute("aria-pressed", "true");

            // Filter media
            const type = tab.dataset.type;
            let count = 0;

            cards.forEach(card => {
                const show = type === "all" || card.dataset.type === type;

                card.hidden = !show;

                if (show) {
                    count++;
                }
            });

            // Empty message
            if (empty) {
                empty.hidden = count !== 0;
            }

        });

    });

});