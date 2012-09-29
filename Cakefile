fs = require('fs')
watch = require('watch')
mustache = require('mustache')
marked = require('marked')

marked.setOptions(
	gfm: true
	pedantic: false
	sanitize: true
	# highlight: (code, lang) ->
	# 	if lang is 'js'
	# 		return javascriptHighlighter(code)

	# 	return code
)

prepare_slide = (slide) ->
	for own key, value of slide
		if typeof value is 'object'
			continue

		if key is 'class'
			continue

		if key is 'markdown'
			try
				slide[key] = marked(fs.readFileSync './src/' + value, 'utf8')
			catch err
				console.log err.stack

			continue

		if key is 'code'
			try
				value = fs.readFileSync './src/' + value, 'utf8'
			catch err
				console.log err.stack

		slide[key] = {}
		slide[key][key] = value

	null

task 'watch', 'Continuously generate the slides', (options) ->
	invoke 'build'

	watch.createMonitor './src', (monitor) ->
		monitor.on "changed", (f, curr, prev) ->
			if f.match /^[^\.]+\.[^\.~]+$/
				console.log f + ' changed'
				invoke 'build'

task 'build', 'Generate the slides', (options) ->
	if not fs.existsSync 'slides'
		fs.mkdirSync 'slides'

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
