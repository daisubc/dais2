---
layout: basic
title: People
description: Meet the UBC DAIS Lab team. Our research group is working on machine learning, data analytics and process control research.
permalink: /people/
---

{% assign y_end = site.time | date: '%Y' %}
{% assign y_start = 2002 %}

{% assign active_members = site.profiles | where_exp:"member", "member.status != 'alumni'" %}
{% assign degrees = "Research Associate|Postdoc|PhD|MASc|MEng|Undergraduate" | split: "|" %}

<h1 class="title">Faculty & Staff</h1>
- **[Dr. {{ site.name }}]({{ site.baseurl }}/about/)**, Principal Investigator
- **[Link to APSC Staff Directory](https://engineering.ubc.ca/about/staff-directory)**

<hr>

{% for degree in degrees %}

<h1 class="title"> {{ degree }} </h1>
<!-- Github pages is still at jekyll 3.9.0, doesnt support binary operators in where_exp yet -->
{% assign members = active_members | where_exp:"member", "member.degree == degree" | sort: 'year_start' | reverse %}

<div class="columns is-multiline">
{% for member in members %}
	<div class="column is-one-third-desktop is-full-mobile">
		<article class="media">
		  <figure class="media-left">
		    <p class="image is-96x96 is-round">
		    	{% if member.img %}
		    		<a href="{{ member.url }}"><img class="is-rounded" style="height: 100%; object-fit: cover;" src="{{ site.baseurl }}/assets/profile/{{ member.img }}" alt="{{ member.title }}"></a>
		    	{% else %}
		    		<a href="{{ member.url }}"><img class="is-rounded" src="https://bulma.io/images/placeholders/128x128.png" alt="Placeholder Profile Image"></a>
		    	{% endif %}	    	
		    </p>
		  </figure>
	  	<div class="media-content">
	    	<div class="content team-member">
	  			<a href="{{ member.url }}" class="member-name">
	  				{% if member.degree == "Postdoc" %}Dr. {% endif %}
	  				<span itemprop="name">{{ member.title }}</span>
		  		</a>
		  		<p class="member-project">{{ member.project }}</p>
		  	</div>
		  </div>
		</article>
	</div>
{% endfor %}
</div>

{% endfor %}

<h1> Alumni </h1>
<p> Former students and visitors </p>

<div class="table-container">
<table class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth">
	<thead>
		<tr>
			<th>Name</th>
			<th>Degree</th>
			<th>Position After Leaving/Now At</th>
		</tr>
	</thead>
	<tbody>	
	{% for y in (y_start..y_end) reversed %}
		{% assign sorted_alum = site.data.alumni | where:"year", y %}	
		{% if sorted_alum.size > 0 %}
			<td colspan="3" style="background-color: #eee;"><b>{{y}}</b></td>
			{% for alum in sorted_alum %}
				<tr>
					<td>{% if alum.url %}
						<a href="{{ alum.url }}">{{ alum.name }}</a>
						{% else %}
						{{ alum.name }}
						{% endif %}
					</td>
					<td>{{ alum.degree }}</td>
					<td>{{ alum.position }}</td>
				</tr>
			{% endfor %} 
		{% endif %}
	{% endfor %}
	</tbody>
</table>
</div>

<p class="is-size-7 has-text-weight-light has-text-grey">
  <span class="tag is-light">Missing Names?</span> Submit a pull request on GitHub to add your information - <a href="https://github.com/daisubc/daisubc.github.io/blob/master/_data/alumni.yml">alumni.yml</a>.
</p>

<small><sup>*</sup><i>My collaborators formally supervised these students but I played a significant role in guiding the research of the respective students.</i></small>

{% include awards.html %}