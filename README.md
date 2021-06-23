# balsys
A cooldown manager for mudlet. 
It has graphical elements that are optional.

# non-graphical
mycooldown = balsys:new({name = 'My Cooldown'}) -- other parameters may be passed here, but most of the time this is enough

mycooldown:spend(8) -- typically within a trigger confirming that the cooldown has begun

mycooldown:balback(8) -- optional in a trigger confirming that the cooldown is up. The 8 second timer started in mycooldown:spend(8) will also call this method.

mycooldown:expect(0.25) -- if you run this when you send the command, it sets the cooldown as off, with a 0.25s timer that will set it back to on/ready. Use this if your scripts need to know the command has been sent and not to spam more, but you cannot be sure the command will go through. myscooldown:spend() will delete the expect timer, essentially copnfirming success. The time is optional and defaults to 0.5.

mycooldown:ready() -- returns true if you can use the ability, false if it has been used and is cooling down.

# running a function at the end of the expect timer, or when the cooldown is up
mycooldown:expect(0.5, function()
    print('expect timer timed out')
  end
  )

mycooldown:spend(3, function()
    print('3 seconds is up, do it again.')
  end
  )

# graphical CD effects
mycooldown:setTargetContainer(container)
Pass that method a geyser object that can be a container.
A new label (self.cdlabel) will be created, 0,0,100%,100% with whatever target container/label as the parent. It will be hidden.
When a cooldown has begun with :spend() this will be shown and a faster timer will calculate the changing CSS and apply it rapidly.

mycooldown:setVisualEffect(effect)
Where 'effect' is radial, conical or linear
These are some stock/premade visual effects, stored in balsys[effect].css and balsys[effect].getcss

mycooldown:setVisuals(css, cssfunc)
This method allows you to define your own visual effects. 'css' is a qss string ready for cssfunc to do some math and then use string.format to build the css for each moment in time that the label effect is updated.

