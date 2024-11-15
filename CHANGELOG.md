# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- Rename `Press` into `JustPress`.
- Rename `Down` into `Press` to avoid collision with `Down` from `bevy_picking`.

## [0.2.0] - 2024-11-03

### Added

- Logging for binding.
- `AccumulateBy` modifier.
- `ActionsData::insert_action` to insert a data for `A`.
- `ActionData::events` to get triggered events from the last update.
- `ActionData::value` to get triggered value from the last update.
- `ActionData::trigger_events` to trigger events based on the last `ActionData::update`.
- `BlockBy::events` to block only events. Could be used for chords to avoid triggering required actions.
- `Deref` for `ActionEvent::kind`.
- `ContextInstances` to public API and methods to get `ActionData` for an action.

### Changed

- All events now separate structs instead of enum.
- Modifiers now accept `ActionsData`.
- Rework `ConditionKind` and the logic around it to make the behavior close to UE.
- Consume inputs only if the action state is not equal to `ActionState::None`.
- Remove world access from conditions and modifiers. This means that you no longer can write game-specific conditions or modifiers. But it's much nicer (and faster) to just do it in observers instead.
- Values from `Input` are now converted to the action-level dimension only after applying all input-level modifiers and conditions. This allows things like mapping the Y-axis of `ActionValue::Axis2D` into an action with `ActionValueDim::Axis1D`.
- Rename `ActionBind::with_axis2d` into `ActionBind::with_xy_axis`.
- Rename `ScaleByDelta` into `DeltaScale`.
- Rename `Released` into `Release`.
- Rename `Pressed` into `Press`.
- Rename `BlockedBy` into `BlockBy`.
- Rename `Scalar` into `Scale`.
- `ActionData::update` now accepts a value and no longer trigger events.
- Use `isize` for `InputContext::PRIORITY`.
- Replace `SmoothDelta` with `LerpDelta` that does only linear interpolation. Using easing functions for inputs doesn't make much sense.
- Modifiers are now allowed to change passed value dimensions.
- All built-in modifiers now handle values of any dimention.
- Replace `with_held_timer` with `relative_speed` that just accepts a boolean.
- Rename `HeldTimer` into `ConditionTimer`.
- Use `trace!` instead of `debug!` for triggered events.

### Removed

- `ignore_incompatible!` since no longer needed.
- `SwizzleAxis::XXX`, `SwizzleAxis::YYY` and `SwizzleAxis::ZZZ`. They encourage a bad pattern of defining actions with duplicate data. Duplicate axes inside the trigger if needed.
- `ActionData::trigger_removed`, use `ActionData::trigger_events` instead.
- `Normalize` modifier, use `DeadZone::default` instead to properly work with analogue inputs.

## [0.1.0] - 2024-10-20

Initial release.

[unreleased]: https://github.com/projectharmonia/bevy_replicon/compare/v0.2.0...HEAD
[0.2.0]: https://github.com/projectharmonia/bevy_replicon/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/projectharmonia/bevy_replicon/releases/tag/v0.1.0
