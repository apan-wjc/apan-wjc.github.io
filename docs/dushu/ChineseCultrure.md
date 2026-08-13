{% if cc.tian_gan %}
  <h3>{{ cc.tian_gan.tg_title }}</h3>
  <p>{{ cc.tian_gan.tg_message }}</p>
  <ol>
    {% for tg_item in cc.tian_gan.tg_items %}
      <li>{{ tg_item }}</li>
    {% endfor %}
  </ol>
{% endif %}

{% if cc.di_zhi %}
  <h3>{{ cc.di_zhi.dz_title }}</h3>
  <p>{{ cc.di_zhi.dz_message }}</p>
  <ol>
    {% for dz_item in cc.di_zhi.dz_items %}
      <li>{{ dz_item }}</li>
    {% endfor %}
  </ol>
{% endif %}

{% if cc.sheng_xiao %}
  <h3>{{ cc.sheng_xiao.sx_title }}</h3>
  <p>{{ cc.sheng_xiao.sx_message }}</p>
  <ol>
    {% for sx_item in cc.sheng_xiao.sx_items %}
      <li>{{ sx_item }}</li>
    {% endfor %}
  </ol>
{% endif %}
