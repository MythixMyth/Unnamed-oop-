# Unnamed OOP!
An unnamed approach to OOP in luau, A faster way.

## DISCLAIMAR: This approach is only for performance, it does not account for memory changes, The memory difference is quite a bit however performance difference is even larger in most cases, Most practical usage would be for singletons, managers or signals.

As beginners we all see people in dev servers like HD , rodevs and others participate in OOP for their luau scripts, especially modules. This approach is usually done by metatables (The easiest way). However the easiest way has proven to be.. incredibly BAD for performance 💔😭.

A great alternative to this `metatable` approach for OOP is this unnamed one I found, Idk the person who first found this so I cant credit them 🤷, It goes somethnig like this

```LUAU
local Human = {
  Speed = 16,
  Health = 100
}

function ApplyDamage(self , Damage)
  self.Health -= Damage
end

return function(Speed : number?)
  local self = table.clone(Human)
  if Speed then self.Speed = Speed end
  return self, {ApplyDamage}
end
```

Ofcourse  you can restructure this into multiple ways, eg using a constructor function instead of returning the function itself, aswell as using a table to store the constructor + other methods like so
```LUAU
local module = {}
local Human = { Speed = 16, Health = 100 }

module.New(Speed : number?)
  local self = table.clone(Human)
  if Speed then self.Speed = Speed end
end

module.ApplyDamage(self, Damage)
  self.Health -= Damage
end

return module
```
