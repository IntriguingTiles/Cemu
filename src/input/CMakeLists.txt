project(CemuInput)

include_directories(".")

add_library(CemuInput
InputManager.cpp
InputManager.h
ControllerFactory.cpp
ControllerFactory.h
api/ControllerState.h
api/Controller.cpp
api/Controller.h
api/ControllerState.cpp
api/InputAPI.h
api/ControllerProvider.h
emulated/ProController.cpp
emulated/EmulatedController.h
emulated/EmulatedController.cpp
emulated/ProController.h
emulated/WPADController.cpp
emulated/WPADController.h
emulated/WiimoteController.h
emulated/VPADController.cpp
emulated/WiimoteController.cpp
emulated/VPADController.h
emulated/ClassicController.cpp
emulated/ClassicController.h
)

set_property(TARGET CemuInput PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")

# SDL
target_sources(CemuInput PRIVATE
api/SDL/SDLController.cpp
api/SDL/SDLControllerProvider.cpp
api/SDL/SDLController.h
api/SDL/SDLControllerProvider.h
)

# DSU
target_sources(CemuInput PRIVATE
api/DSU/DSUController.h
api/DSU/DSUControllerProvider.cpp
api/DSU/DSUController.cpp
api/DSU/DSUControllerProvider.h
api/DSU/DSUMessages.h
api/DSU/DSUMessages.cpp
)

# Keyboard controller
target_sources(CemuInput PRIVATE
api/Keyboard/KeyboardControllerProvider.h
api/Keyboard/KeyboardControllerProvider.cpp
api/Keyboard/KeyboardController.cpp
api/Keyboard/KeyboardController.h
)

# Native gamecube
target_sources(CemuInput PRIVATE
api/GameCube/GameCubeController.cpp
api/GameCube/GameCubeControllerProvider.h
api/GameCube/GameCubeControllerProvider.cpp
api/GameCube/GameCubeController.h
)

if(WIN32)
# Native wiimote (Win32 only for now)
target_sources(CemuInput PRIVATE
api/Wiimote/WiimoteControllerProvider.h
api/Wiimote/windows/WinWiimoteDevice.cpp
api/Wiimote/windows/WinWiimoteDevice.h
api/Wiimote/WiimoteControllerProvider.cpp
api/Wiimote/WiimoteMessages.h
api/Wiimote/NativeWiimoteController.h
api/Wiimote/NativeWiimoteController.cpp
api/Wiimote/WiimoteDevice.h
)

# XInput
target_sources(CemuInput PRIVATE
api/XInput/XInputControllerProvider.cpp
api/XInput/XInputControllerProvider.h
api/XInput/XInputController.cpp
api/XInput/XInputController.h
)

# DirectInput
target_sources(CemuInput PRIVATE
api/DirectInput/DirectInputControllerProvider.cpp
api/DirectInput/DirectInputController.h
api/DirectInput/DirectInputControllerProvider.h
api/DirectInput/DirectInputController.cpp
)
endif()

target_precompile_headers(CemuInput PRIVATE ../Common/precompiled.h)

target_include_directories(CemuInput PRIVATE ../)
