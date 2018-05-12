# Peachy
A parser/renderer for Aseprite animations in LÖVE.

# How to use
Draw some animations in Aseprite and export the file as a spritesheet:
![Aseprite export](docs/img/aseprite_export.png)

Make sure that you export JSON data with frame tags.

```lua
-- Load an aseprite animation file called spinner.json, with the image
-- spinner.png & start with the animation tag "Spin"
spinner = peachy.new("spinner.json", love.graphics.newImage("spinner.png"), "Spin")

function love.draw()
  -- Draw at 50,50
  spinner:draw(50, 50)
end

function love.update(dt)
  spinner:update(dt)
end
```

If you don't specify an image to load in new by passing nil or false as the second argument, then peachy will attempt to load the image specified in the data file. This can cause problems: see limitations below.

# Examples
See main.lua for further examples.

# Limitations
* By default Aseprite will export a **non-relative** path as the image file. This is problematic because LÖVE will refuse to load it and it's non-portable. There's a workaround listed [here](https://github.com/aseprite/aseprite/issues/1606). Either specify the image yourself in `peachy.new`, edit the JSON manually or use the CLI.
* Exported sprite sheets **must** be exported as an array, **not** as a hash table.

![Export as array](docs/img/export_type.png)