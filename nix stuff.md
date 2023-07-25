stuff I want to do
- [ ] configure my own home manager
- [ ] use the clearpath nix ros wrapper / packager

### nix notes

a kind of hacky way to see if you are in a nix shell is to echo the $PATH and see if there are any nix store paths within it.

opengl stuff within nix can be weird, especially in non-NixOS environments and google has a hard time finding the solutions that the nix wiki has for 

"Error: couldn't find RGB GLX visual or fbconfig"

https://nixos.wiki/wiki/Nixpkgs_with_OpenGL_on_non-NixOS can provide the solution

`nixGL` has worked for me, however getting the built in nvidia graphics card has been a challenge on wsl2 and currently does not work correctly...


links to blogs / resources:
https://ianthehenry.com/posts/how-to-learn-nix/introduction/
https://serokell.io/blog/practical-nix-flakes

https://github.com/the-nix-way
- more than just home manager
- includes project templates n shit
### nix capabilities
- nix can work with docker
    - nix can build docker images (`nixpkgsUnstable.dockerTools`)
### nix commands
`nix flake show`: shows what is in the nix flake

`nix run`: will build and run what outputs from the build

`nix develop`: will provide a shell in which has all of the dependencies installed and we can just use our normal build workflow of making the build dir, running `cmake` and `make`

`nix build --rebuild` will force a rebuild of a flake

`-L`: big logs instead of single line log --> doesnt work? TODO figure out
    -- it actually does work

### nix flakes

development helpers:
https://github.com/danielbarter/mini_compile_commands

enabling flakes:

inputs = dependencies

`let` & `in`
anything after let and before in are variable declarations and anything after in within the next set can use those variables.

`with asdf` = `using namespace asdf`

`<input-package>.follows = <other-package>` means that the package will use the other packages inputs first I believe, then it will also include its required ones. I think that means that it will use the same version of an input that is required for both the following input package and the other package?

### nix language

anything with `{ }` is a set or a list of key value pairs.

adding `rec` to a set allows the set to reference itself, or use parts of itself.   


### nix home manager
- initial setup:
	- install nix / enable flakes yada yada yada
	- next steps (https://nix-community.github.io/home-manager/index.html#sec-install-standalone) for setting up home manager INITIALLY without my `home.nix`
		1. `nix-channel --add https://github.com/nix-community/home-manager/archive/master.tar.gz home-manager`
		2. `nix-channel --update`
		3. `nix-shell '<home-manager>' -A install`
	- I want to use flakes for my home manager stuff, so next I can do this:
		4. `nix run home-manager/release-23.05 -- init --switch`
			- (i can actually prob just use this connect instead step 3)
	- 
	- on my home computer's wsl my home is at `/home/neb/.config/home-manager/home.nix`
	- 
- option search: https://mipmip.github.io/home-manager-option-search/
	- https://nix-community.github.io/home-manager/options.html