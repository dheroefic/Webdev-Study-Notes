---
group: ember
layout: post

title: Models
descr: Using Ember models to better structure data
---

Models are how Ember manages properties of data objects. These are most frequently used with data coming from an API or other third-party, and controlled using the `ember-data` add-on. The basic setup of one looks like this:

{% highlight javascript %}{% raw %}
import DS from 'ember-data';

export default DS.Model.extend({
  name     : DS.attr('string'),
  age      : DS.attr('integer'),
  alive    : DS.attr('boolean'),
  children : DS.hasMany('child'),
  parent   : DS.belongsTo()
});
{% endraw %}{% endhighlight %}

Models can also use computed properties in case some values must be created using others. The properties put in as arguments, whenever they change, will update the computed properties. Just **don't change any values within computed properties!**

{% highlight javascript %}{% raw %}
import { computed } from '@ember/object';

  full_name: computed('first_name', 'last_name', function(){
    return `Hello, my name is ${this.get('first_name')} ${this.get('last_name')}`;
  })
{% endraw %}{% endhighlight %}
