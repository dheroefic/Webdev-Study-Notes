---
group: ember
layout: post

title: Routes
descr: An explaination of Ember routes and their basic uses
---

The `model` function is what's used to get info from the data source and is passed onto the controller. Reference it in the controllers and templates by using the `model` variable.

Get any current parameters in the URL by referencing them in the `model()` function.

{% highlight javascript %}{% raw %}
import Route from '@ember/routing/route';

export default Route.extend({
  model: function(params) {

    let parameter = params.parameter_id; // Defined in the router
  }
});
{% endraw %}{% endhighlight %}

Specific routes can be [assigned to certain paths](https://emberigniter.com/building-user-interface-around-ember-data-app/) in the main router file:

{% highlight javascript %}{% raw %}
Router.map(function() {
  this.route('books', { path: '/' });
  this.route('author', { path: '/author/:author_id' });
});
{% endraw %}{% endhighlight %}

Route parameters are the ones with the colon prepended. They can be accessed in the model by including the `params` argument in the function.

{% highlight javascript %}{% raw %}
model(params) {
  return this.store.findRecord('author', params.author_id);
}
{% endraw %}{% endhighlight %}

You can also grab values set or computed in the controller with the below method. This is great for creating router actions bound to values calculated in the controller, such as calculating if all items in a model have been displayed.

{% highlight javascript %}{% raw %}
this.controllerFor('<controller_name>').get('<property_name>');
{% endraw %}{% endhighlight %}

## Loading Multiple Models

If you need to load multiple models as a single promise object, the `RSVP.hash` tool lets you do this. It accepts a hash, where each value is a promise. This way you can have a promise activate once all the promises are resolved, such as a loading screen being toggled off.

{% highlight javascript %}{% raw %}
import { hash } from 'rsvp';

model(params) {
  return hash({
    character: this.store.findRecord('character', params.character),
    teams: this.store.findAll('team')
  });
}
{% endraw %}{% endhighlight %}
