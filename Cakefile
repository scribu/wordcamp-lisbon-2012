fs = require('fs')
mkdirp = require('mkdirp').sync
mustache = require('mustache')

task 'build', 'Generate the slides', (options) ->
	mkdirp 'slides'

	data = JSON.parse(fs.readFileSync 'slides.json', 'utf8')

	for slide in data['slides']
		if slide.code?
			slide.code = fs.readFileSync slide.code, 'utf8'

	template = fs.readFileSync 'template.html', 'utf8'

	output = mustache.render(template, data)

	fs.writeFileSync 'slides/index.html', output

	console.log output
