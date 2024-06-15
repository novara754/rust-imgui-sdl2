# imgui-sdl2

> This is a fork of [michaelfairley/rust-imgui-sdl2](https://github.com/michaelfairley/rust-imgui-sdl2)
> the uses the latest version of imgui straight from GitHub.
> It also uses my version of the imgui-opengl-renderer crate.

[SDL2](https://github.com/Rust-SDL2/rust-sdl2) Input handling for [imgui-rs](https://github.com/Gekkio/imgui-rs)

## Integration guide

1. Construct it.
   ```rust
   let mut imgui_sdl2 = imgui_sdl2::ImguiSdl2::new(&mut imgui, &window);
   ```
2. At the top of your event handling loop, pass in the input events, and ignore the ones that imgui has captured.
   ```rust
   imgui_sdl2.handle_event(&mut imgui, &event);
   if imgui_sdl2.ignore_event(&event) { continue; }
   ```
3. Call `prepare_frame` before calling `imgui.frame()`.
   ```rust
   imgui_sdl2.prepare_frame(imgui.io_mut(), &window, &event_pump.mouse_state());
   ```
4. Call `prepare_render` immediately before your UI rendering code.
   ```rust
   imgui_sdl2.prepare_render(&ui, &window);
   ```

Take a look at the [example app](./examples/demo.rs) to see it all in context.
