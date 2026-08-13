<style>
.hover-container {
  position: relative;
}
.hover-image {
  display: none;
  position: fixed;
  top: 80px;
  right: 150px;
  max-width: 500px;
  max-height: 500px;
  z-index: 99999;
  border-radius: 8px;
  box-shadow: 0 8px 24px rgba(0,0,0,.4);
  background: white;
}
.hover-container:hover .hover-image {
  display: block;
}
</style>

<table>
  <thead>
    <tr>
      <th>Set Number</th>
      <th>Set Name</th>
      <th>Purchase Date</th>
      <th>Price</th>
      <th>Order</th>
    </tr>
  </thead>
  <tbody>
    {% for set in lgj.lego_sets | sort(attribute='order', reverse=true) %}
    <tr>
      <td><a href="{{ set.url }}">{{ set.set_number }}</a></td>
      <td>
        <div class="hover-container">
          <a href="{{ set.image }}" target="_blank" class="set-name">{{ set.set_name }}</a>
          <img src="{{ set.image }}" class="hover-image" alt="{{ set.set_name }}">
        </div>
      </td>
      <td>{{ set.purchase_date }}</td>
      <td>{{ set.price }}</td>
      <td>{{ set.order }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>
