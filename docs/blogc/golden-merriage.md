---
icon: material/heart
hide: toc
title: 金婚
tags:
  - 备忘
---
金婚前与 YY 共走 50 个地方。

<style>

.md-content {
  max-width: none;
}
.md-grid {
  max-width: 1400px;  /* adjust to taste — default is usually ~1200px */
}

/* Dark mode striping (white overlay) */
[data-md-color-scheme="slate"] .travel-table tr:nth-child(even) {
  background-color: rgba(255, 255, 255, 0.04);
}
[data-md-color-scheme="slate"] .travel-table tr:hover {
  background-color: rgba(255, 255, 255, 0.08);
}

/* Light mode striping (dark overlay) */
[data-md-color-scheme="default"] .travel-table tr:nth-child(even) {
  background-color: rgba(0, 0, 0, 0.05);
}
[data-md-color-scheme="default"] .travel-table tr:hover {
  background-color: rgba(0, 0, 0, 0.09);
}

.travel-table tr:nth-child(odd) {
  background-color: transparent;
}

.travel-table {
  font-size: 0.8em;
}
</style>

<table class="travel-table">
  <thead>
    <tr>
      <th>No.</th>
      <th>Date</th>
      <th>Destination</th>
      <th>Region</th>
      <th>Country</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    {% for trip in gm.travels | sort(attribute='number', reverse=true) %}
    <tr>
      <td>{{ trip.number }}</td>
      <td>{{ trip.date }}</td>
      <td>{{ trip.destination }}</td>
      <td>{{ trip.region }}</td>
      <td>{{ trip.country }}</td>
      <td>{{ trip.notes }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>
