document.addEventListener("DOMContentLoaded", () => {
  const marketPhrases = [
    "Away with you!",
    "Vanish into the moonlight!",
    "Return to the shadows!",
    "Begone, strange traveler!",
    "Disappear, creature!",
    "Back to the night!",
    "Hide your magic!",
    "Return to the realm unseen!",
    "Step beyond the veil!",
    "Fly from this world!"
  ];

  const sections = document.querySelectorAll("section");
  const removed = [];

  // Create “banish” buttons
  sections.forEach(section => {
    const btn = document.createElement("button");
    btn.className = "banish";
    btn.textContent = marketPhrases[Math.floor(Math.random() * marketPhrases.length)];
    section.prepend(btn);
  });

  // Create restore button
  const restoreBtn = document.createElement("button");
  restoreBtn.id = "restore";
  restoreBtn.textContent = "Restore Creatures";
  document.querySelector("header")?.appendChild(restoreBtn);

  // Banish section
  document.addEventListener("click", e => {
    if (e.target.matches(".banish")) {
      const sec = e.target.closest("section");
      removed.push(sec.outerHTML);

      sec.style.transition = "opacity 0.3s ease, transform 0.3s ease";
      sec.style.opacity = 0;
      sec.style.transform = "scale(0.96)";

      setTimeout(() => sec.remove(), 300);
    }
  });

  // Restore handler
  restoreBtn.addEventListener("click", () => {
    if (!removed.length) return;
    const container = document.querySelector("header");
    removed.forEach(html => {
      container.insertAdjacentHTML("beforeend", html);
    });
    removed.length = 0;
  });
});
