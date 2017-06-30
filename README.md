# QDSpontaneous
QDSpontaneous is a library that allows Mage and Bard kits  to cast spells spontaneously, like Sorcerers in the Enhanced Infinity Engine. 

## Background
Sorcerers are often viewed as superior to their Mage counterparts in terms of total spellcasting power. Thus, it is not surprising that requests to be able to multiclass Sorcerers have been made since at least 2004 (although probably earlier). Unfortunately, multi-classing Sorcerers is still not possible (due presumably to rather stubborn hardcoding within the engine). Furthermore, later editions of Dungeons and Dragons, allowed all casters to cast spontaneously, with varying restrictions on how many spells they could know or prepare, and how many spells they could cast. 

This library enables mage and bard kits to cast any combination of their prepared spells at a given level. It can be applied selectively on a kit-by-kit basis as desired.  

## Usage
If you would like to tie your mod's spontaneous arcane casters into this framework, then you first need to download the latest version of the qdspontaneous.tpa file (located in Sorcery/lib) and the QDBLANK.spl file (located in Sorcery/data) and include these somewhere in your mod's installation files. Both files may be kept anywhere within your mod's installation folder, but they must both be present for this library to function. 

In addition, you must include a .tra file with these strings (translated into the desired language) at these exact positions: 
<pre>@10000001 = ~Remaining Level %lvl% Mage Spells: %slots%~ 
@10000002 = ~Remaining Level %lvl% Priest Spells: %slots%~ 
</pre>

After completing these two tasks, you can enable the functionality in your mod's compenents by adding the following code to your mod's installation files (either .tp2 or .tpa). 


These lines should be included after you use the ADD_KIT function (if you are adding a new kit). 
<pre>INCLUDE ~Your/Mod/Structure/qd_spontaneous.tpa~ 
 
LAF qd_spontaneous 
	STR_VAR 
    kit_clab = ~kitclab~ //the internal name of your kit's clab file, without the .2da extension  
		kit_prefix = ~XXYYYY~ //a string of up to 6 characters beginning with your modder prefix 
		known_prog = ~Your/File/Structure/TABLE~ //a .2da file, without the extension, that says how many spells the kit should have access to at each level (defaults to SPLSRCKN.2da)
		casts_prog = ~Your/File/Structure/OTHERTBL~ //a .2da file, without the extension, that says how many spells of each level the kit should be able to cast (defaults to MXSPLSRC.2da) 
		lib_dir = ~Your/File/Structure~ //the folder, without the final "/" containing QDBLANK.spl 
END 
</pre>

Once you've finished installing all kits that will use this system also include the following code in a standalone component. Be sure to install this component after all mods that 1) add items that increase arcane spell slots, 2) add new arcane spells, or 3) add kits that utilize this functionality. Failure to follow this may result in strange behavior when using this system. 

<pre>INCLUDE ~Your/Mod/Structure/qd_spontaneous.tpa~  
LAF qd_spontaneous.patch_items END 
LAF qd_spontaneous.patch_spells END 
</pre> 

### Limitations
This system, as it is emulating a spontaneous casting system within the Mage spellbook interface, has two major drawbacks to my knowlege. The first is that you must prepare a single copy of each spell you wish to have available for casting and then complete a rest in order to cast your spells initially. Secondly, the game will not display how many more casts of each level within the spell bar itself; to make up for this, whenever a character casts a spell, a line is printed to the combat log saying how many more spells of that level they may cast before resting.

Effects that recharge spell slots or grant additional spell slots may seem to not work or even cause the system to break. I will do my best to minimize the weird behavior of these effects. 

### Applications
This library is very versatile, and can be used in a variety of scenarios. Some of the things it can do include: 
* emulating Sorcerer as a Mage kit. 
* enabling emulation of multi- or dual-classed Sorcerers (e.g. Fighter/Sorcerer). 

## QDSpontaneous in Action
No mods make use of QDSpontaneous yet; be the first!

## Permissions and Support 
I am publishing QDSpontaneous so that other modders may make spontaneously casting Mage or Bard kits with ease. I do not require nor expect modders to contact me requesting permission to use this library. If you encounter errors while using this library, please contact me so that I may provide fixes and updates. 
