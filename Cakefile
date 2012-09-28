fs = require('fs')
mkdirp = require('mkdirp').sync
watch = require('watch')
mustache = require('mustache')

prepare_slide = (slide) ->
	for own key, value of slide
		if typeof value is 'object'
			continue

		if key is 'class'
			continue

		if key is 'code'
			try
				value = fs.readFileSync value, 'utf8'
			catch err
				console.log err.stack

		slide[key] = {}
		slide[key][key] = value

	null

task 'watch', 'Continuously generate the slides', (options) ->
	invoke 'build'

	watch.createMonitor './src', (monitor) ->
		monitor.on "changed", (f, curr, prev) ->
			if f in ['src/template.html', 'src/slides.json']
				console.log f + ' changed'
				invoke 'build'

task 'build', 'Generate the slides', (options) ->
	mkdirp 'slides'

	raw_data = fs.readFileSync './src/slides.json', 'utf8'

	try
		data = JSON.parse raw_data
	catch err
		console.log err.stack
		return

	for slide in data['slides']
		prepare_slide slide

	template = fs.readFileSync './src/template.html', 'utf8'

	output = mustache.render(template, data)

	fs.writeFileSync 'slides/index.html', output
