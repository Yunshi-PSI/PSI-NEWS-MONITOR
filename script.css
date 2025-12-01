/**
 * Manitoba PSE News Monitor – front-end script
 * Reads data/news.json and renders three sections: Manitoba, Canada, World.
 */

async function loadNews() {
  const mbList = document.getElementById("mb-list");
  const caList = document.getElementById("ca-list");
  const worldList = document.getElementById("world-list");
  const lastUpdatedEl = document.getElementById("last-updated");

  try {
    const response = await fetch("data/news.json", {
      cache: "no-store" // helps prevent stale files on some browsers
    });

    if (!response.ok) {
      throw new Error(`HTTP error ${response.status}`);
    }

    const data = await response.json();

    // Update "Last updated" time if available
    if (data.generated_at && lastUpdatedEl) {
      lastUpdatedEl.textContent = `Last updated: ${data.generated_at}`;
    }

    renderSection(mbList, data.manitoba || []);
    renderSection(caList, data.canada || []);
    renderSection(worldList, data.world || []);
  } catch (error) {
    console.error("Failed to load news.json:", error);
    showError(mbList);
    showError(caList);
    showError(worldList);
    if (lastUpdatedEl && !lastUpdatedEl.textContent) {
      lastUpdatedEl.textContent = "Unable to load latest news (data file error).";
    }
  }
}

/**
 * Render an array of news items into a container.
 */
function renderSection(container, items) {
  if (!container) return;

  container.innerHTML = "";

  if (!items.length) {
    const p = document.createElement("p");
    p.className = "placeholder";
    p.textContent = "No recent articles found in this category.";
    container.appendChild(p);
    return;
  }

  for (const item of items) {
    const card = document.createElement("article");
    card.className = "news-card";

    const meta = document.createElement("div");
    meta.className = "news-meta";

    const outletSpan = document.createElement("span");
    outletSpan.className = "badge-outlet";
    outletSpan.textContent = item.outlet || "Unknown outlet";

    const dateSpan = document.createElement("span");
    dateSpan.className = "badge-date";
    dateSpan.textContent = item.date || "Unknown date";

    meta.appendChild(outletSpan);
    meta.appendChild(dateSpan);

    const link = document.createElement("a");
    link.className = "news-link";
    link.href = item.url || "#";
    link.target = "_blank";
    link.rel = "noopener noreferrer";
    link.textContent = item.headline || "Untitled article";

    const summaryP = document.createElement("p");
    summaryP.className = "news-summary";
    summaryP.textContent = item.summary || "";

    card.appendChild(meta);
    card.appendChild(link);
    card.appendChild(summaryP);

    container.appendChild(card);
  }
}

/**
 * Show a generic error message for a section if fetch fails.
 */
function showError(container) {
  if (!container) return;
  container.innerHTML = "";
  const p = document.createElement("p");
  p.className = "error-message";
  p.textContent = "Unable to load news for this section. Please try again later.";
  container.appendChild(p);
}

// Run after HTML has loaded (script is included with defer in index.html)
loadNews();
