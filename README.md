# lingua-franca
set of high level conventions that allow python libraries to speak the same 'language'

## Use case

Let's say you want to  lighten a color defined in a css token and apply it as the background
of a text field. We will use the [tinycss](https://pypi.org/project/tinycss/), 
[colour](https://pypi.org/project/colour/) and
[tkinter](https://docs.python.org/fr/3.8/library/tkinter.html) libraries.

This could be achieved with the following _untested_ code:

```python
css_color = tinycss.color3.parse_color(token)
color = colour.Color(rgb=css_color[:3])
color.saturation = .5
label = tkinter.Label(root, text="Hello", background=color.hex)
```

This code is not really good, with boilerplate and resource waste for converting between objects.
And the developer needed to study the color object model of the three libraries.

If the libraries understood the color protocol we could achieve a much better code:

```python
color = tinycss.color3.parse_color(token, factory=colour.Color)
color.saturation = .5
label = tkinter.Label(root, text="Hello", background=color)
```
## Usage
See  the [wiki](https://github.com/sebkeim/lingua-franca/wiki)
