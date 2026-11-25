document.addEventListener("DOMContentLoaded", () => {
    console.log("G12 Biology Project is ready.");

    const menu = document.querySelector(".menu-toggle");
    const nav = document.querySelector(".nav-links");
    const btn = document.getElementById("resourceBtn");
    const drop = document.getElementById("resourceMenu");

    // Mobile navigation
    if (menu && nav) {
        menu.addEventListener("click", () => {
            const open = nav.classList.toggle("open");
            menu.setAttribute("aria-expanded", String(open));
        });
    }

    // Resources dropdown
    if (btn && drop) {
        btn.addEventListener("click", event => {
            event.stopPropagation();

            const open = drop.classList.toggle("show");
            btn.setAttribute("aria-expanded", String(open));
        });

        document.addEventListener("click", event => {
            if (!event.target.closest(".dropdown")) {
                drop.classList.remove("show");
                btn.setAttribute("aria-expanded", "false");
            }
        });
    }

    // Active navigation
    const current = location.pathname.split("/").pop() || "index.html";

    document.querySelectorAll("[data-page]").forEach(link => {
        if (link.dataset.page === current) {
            link.classList.add("active");
            link.setAttribute("aria-current", "page");
        }
    });
});

/* ==============================
   3D PLANT INTERACTION
============================== */

document.addEventListener("DOMContentLoaded", () => {

    const plant = document.getElementById("plantAnimation");

    if (!plant) return;

    const isMobile = window.matchMedia(
        "(max-width: 768px)"
    ).matches;

    const reduceMotion = window.matchMedia(
        "(prefers-reduced-motion: reduce)"
    ).matches;

    if (isMobile || reduceMotion) return;

    plant.addEventListener("mousemove", (event) => {

        const rect = plant.getBoundingClientRect();

        const x = event.clientX - rect.left;
        const y = event.clientY - rect.top;

        const centerX = rect.width / 2;
        const centerY = rect.height / 2;

        const rotateY = (x - centerX) / 20;
        const rotateX = (centerY - y) / 20;

        plant.style.transform =
            `rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
    });

    plant.addEventListener("mouseleave", () => {
        plant.style.transform =
            "rotateX(0deg) rotateY(0deg)";
    });

});