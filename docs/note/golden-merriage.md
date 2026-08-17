---
icon: material/heart
hide: toc
title: 金婚
tags:
  - 备忘
---
金婚前与 YY 共走 50 个地方。

<style>
/* Dark mode striping (white overlay) */
[data-md-color-scheme="slate"] table tr:nth-child(even) {
  background-color: rgba(255, 255, 255, 0.04);
}
[data-md-color-scheme="slate"] table tr:hover {
  background-color: rgba(255, 255, 255, 0.08);
}
/* Light mode striping (dark overlay) */
[data-md-color-scheme="default"] table tr:nth-child(even) {
  background-color: rgba(0, 0, 0, 0.05);
}
[data-md-color-scheme="default"] table tr:hover {
  background-color: rgba(0, 0, 0, 0.09);
}
table tr:nth-child(odd) {
  background-color: transparent;
}
</style>

<table>
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
