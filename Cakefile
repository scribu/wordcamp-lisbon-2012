fs = require('fs')
mkdirp = require('mkdirp').sync
Handlebars = require('handlebars')

Handlebars.registerHelper 'include', (path) ->
	fs.readFileSync path, 'utf8'

task 'build', 'Generate the slides', (options) ->
	mkdirp 'slides'

	data = JSON.parse(fs.readFileSync 'slides.json', 'utf8')

	for slide in data['slides']
		if slide.code?
			slide.code = fs.readFileSync slide.code, 'utf8'

	template = Handlebars.compile(fs.readFileSync 'template.html', 'utf8')

	fs.writeFileSync 'slides/index.html', template(data)

	console.log template(data)
