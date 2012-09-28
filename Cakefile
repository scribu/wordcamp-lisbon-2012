fs = require('fs')
mkdirp = require('mkdirp').sync
watch = require('watch')
mustache = require('mustache')

prepare_slide = (slide) ->
	for own key, value of slide
		if key in 'list'
			continue

		if key is 'code'
			value = fs.readFileSync value, 'utf8'

		slide[key] = {}
		slide[key][key] = value

	null

task 'watch', 'Continuously generate the slides', (options) ->
	watch.createMonitor '.', (monitor) ->
		monitor.on "changed", (f, curr, prev) ->
			if f in ['template.html', 'slides.json']
				console.log f + ' changed'
				invoke 'build'

task 'build', 'Generate the slides', (options) ->
	mkdirp 'slides'

	data = JSON.parse(fs.readFileSync 'slides.json', 'utf8')

	for slide in data['slides']
		prepare_slide slide

	template = fs.readFileSync 'template.html', 'utf8'

	output = mustache.render(template, data)

	fs.writeFileSync 'slides/index.html', output
