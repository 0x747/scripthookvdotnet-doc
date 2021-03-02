#  Getting started with ScriptHookVDotNet

Before you can start playing with ScriptHookVDotNet you need some prerequisites:
* GTA V
* [ScriptHookV](http://www.dev-c.com/gtav/scripthookv/)
* [ScriptHookVDotNet SDK](https://github.com/crosire/scripthookvdotnet)

# How to install ScriptHookVDotNet

1. Download the latest GitHub revision and compile it using Microsoft Visual Studio.
2. Copy `ScriptHookVDotNet.asi` and `ScriptHookVDotNet2/3.dll` to your GTA V directory.
3. Create a `scripts` folder in your GTA V directory (if not already happened).

**Hint**: _ScriptHookVDotNet supports compiled assemblies as well as C# or VB source files which all have to be placed into the `scripts` folder in your GTA V directory._

# Basic Knowledge

Every mod/script you write must inherit from the `Script` class. This class provides 3 events:
* `Tick`
* `KeyUp`
* `KeyDown`

Those 3 events provides the basic work area you can perfectly work with.

# Speeding up Development

To avoid needing to constantly stop and start GTA V, you can use the script reloader in the ScriptHookVDotNet.

* Start GTA
* Test out your scripts
* Alt-tab back to your development environment (Visual Studio)
* Make some changes
* Build the script again
* Copy the DLL file into the `scripts` folder in your GTA V directory
* Alt-tab back into the game
* And **press Insert to load the new script dll**.

_**Note**: This also works with non compiled .cs or .vb files_

You may also want to set up a post build event in Visual Studio to copy the compiled DLL to your scripts folder automatically.

# Code example

Below you can find a basic sample mod that creates a vehicle in front of the own character perfectly heading 90° to the character to get on the car like a sir when pressing **Numpad1**.

**Note**: This script is against SHVDN v3 API.

```cs
using System;
using System.Drawing;
using System.Windows.Forms;
using GTA;

public class CreateVehicle : Script
{
    public CreateVehicle()
    {
        Tick += OnTick;
        KeyUp += OnKeyUp;
        KeyDown += OnKeyDown;
    }

    private void OnTick(object sender, EventArgs e)
    {
    }

    private void OnKeyDown(object sender, KeyEventArgs e)
    {
    }

    private void OnKeyUp(object sender, KeyEventArgs e)
    {
        if (e.KeyCode == Keys.NumPad1)
        {
            Vehicle vehicle = World.CreateVehicle(VehicleHash.Zentorno, Game.Player.Character.Position + Game.Player.Character.ForwardVector * 3.0f, Game.Player.Character.Heading + 90);
            vehicle.CanTiresBurst = false;
            vehicle.Mods.CustomPrimaryColor = Color.FromArgb(38, 38, 38);
            vehicle.Mods.CustomSecondaryColor = Color.DarkOrange;
            vehicle.PlaceOnGround();
            vehicle.Mods.LicensePlate = "SHVDN";
        }
    }
}
```

# Further Reading

[Code Snippets](https://github.com/crosire/scripthookvdotnet/wiki/Code-Snippets)

[How-To Guides](https://github.com/crosire/scripthookvdotnet/wiki/How-Tos)

[Calling Native C++ Hash Functions](https://github.com/crosire/scripthookvdotnet/wiki/How-Tos#calling-native-c-hash-functions)

***

Now feel free to try out new things. There is already so much powerful stuff to play with.