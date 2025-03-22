```python
# Define a constant for the URL template of the div2html service
# This URL is used to render dialogs into HTML format.
# The placeholder `{}` will be replaced with the actual URL of the dialog content.
DIV_2HTML_URL = 'http://div2html.s3.yandex.net/test/dialog.html?url={}'

# Define a constant for the URL template of the div2_2html service
# This URL is used for an alternative or secondary rendering service.
# The placeholder `{}` will be replaced with the actual URL of the dialog content.
DIV2_2HTML_URL = 'http://div2html.s3.yandex.net/div2_2.html?url={}'
```

# EXAMPLE
```python
dialog_url = "http://example.com/dialog.json"
full_url = DIV_2HTML_URL.format(dialog_url)
```

# This would result in 
```full_url``` being ```http://div2html.s3.yandex.net/test/dialog.html?url=http://example.com/dialog.json```

