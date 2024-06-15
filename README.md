local screensize = vec2(ac.getSim().windowWidth, ac.getSim().windowHeight)
local timer = 5
 
-- image_0 is used as the rules splash screen
local image_0 = {
    ['src'] = 'https://i.postimg.cc/W1KmB4z8/408-1000.gif',
    ['sizeX'] = 512, -- size of your image in pixels
    ['sizeY'] = 512, -- size of your image in pixels
    ['paddingX'] = (screensize.x - 512) / 2, -- center horizontally
    ['paddingY'] = screensize.y - 512 - 100 -- 100 pixels from the bottom
}
 
-- image_1 is used as the icon
local image_1 = {
    ['src'] = 'https://i.postimg.cc/CLMSkCqx/dababy.jpg',
    ['sizeX'] = 128,
    ['sizeY'] = 128,
    ['paddingX'] = screensize.x - 128 - 50, -- align it 50 pixels from the right side
    ['paddingY'] = 50 -- align it 50 pixels from the top
}
 
-- this waits for the driver to not be in the setup screen, then starts the timer for the rule splash image
function script.update(dt)
    ac.debug('isInMainMenu', ac.getSim().isInMainMenu)
    if not ac.getSim().isInMainMenu then
        if timer >= 0 then
            timer = timer - dt
        end
    end
end
 
-- this draws the splash screen then after draws the icon
function script.drawUI()
    if timer >= 0 and not ac.getSim().isInMainMenu then
        ui.drawImage(image_0.src, vec2(image_0.paddingX, image_0.paddingY), vec2(image_0.sizeX + image_0.paddingX, image_0.sizeY + image_0.paddingY), true)
    end
    if timer <= 0 then
        ui.drawImage(image_1.src, vec2(image_1.paddingX, image_1.paddingY), vec2(image_1.sizeX + image_1.paddingX, image_1.sizeY + image_1.paddingY), true)
    end
end
