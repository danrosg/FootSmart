
# Change Log
## [1.2.0]
- Fixed: backup grammar rejected valid backups from newer firmware/editor versions that populate previously-unmodeled fields:
  - Bank `pageLimit` field
  - Preset `shiftName` (shifted-display label) - now round-trips through both the backup grammar and the simple grammar/model instead of being forced empty
  - Omniport (expression/aux jack) per-port type and calibration bytes - added a proper `Omniport` model instead of requiring all-default values
  - Top-level backup `description` field - now captured instead of forced empty
- Fixed: a preset/bank message list with a non-contiguous gap (an "unused" slot between two real messages) crashed `--backup-to-simple` with a `switch_dict_bad_switch` error. Added the missing case, and fixed a related crash in `grammar.py`'s `DictBase.gen_keys` when a switch dict's model is `None`.
- Fixed: silent data loss on round-trip for a few message types that only had part of their raw data modeled:
  - PC messages now preserve their second data byte (`extra_byte`) instead of dropping it
  - Bank-level "Set Toggle" messages now preserve bytes beyond the documented preset bitmap (`extra_data`)
  - Bank-level "MIDI Clock" messages now preserve bytes beyond bpm/flags (`extra_data`), and now read/restore bpm even when the clock is stopped (previously only read when not stopped, even though present in the data)
- All fixes verified with a full byte-for-byte round-trip fidelity check (backup -> simple -> backup) against real 128-bank exports from a MC6 Pro on firmware 3.13.6.
## [1.1.0]
- Added controller/global settings for messages, groups, and initializing
## [1.0.1] - 2025-03-13
- All group messages now use engage preset, and a bank at the end
## [1.0.0] - 2025-01-30 NAMM Version
- Config.yaml: created consistent approach to colors with palettes
- Config.yaml: more documentation in file
- Config.yaml: removed unused messages (formerly used in cycle/scrolls)
- Config.yaml: H9 Chorus parameters mapped out
- Config.yaml: Added Singular Sound's Aeros message definitions
- Added cycle preset type, and used it in Config.yaml
- Added empty preset for spacing
- Fixed enable/bypass bug
- Clean up README.md
- Renamed main app footsmart
- Added show option to cycle presets
- Added Delay message
- Added followup modifier (like setup, but after)
- Fixed bug: bank messages have different names/number pairs than preset messages
## [0.4.0] - 2024-12-30
- Cleaned up Example.yaml
- scroll preset (formerly cycle presets) presets can now handle more than 1 message, but all must be the same length
- Renamed cycle to scroll, in preparation for a true cycle
- Implemented cycle presets, which cycle through various values for CC messages
## [0.3.2] - 2024-11-16
- *Press* and *On Bank Entry* are now defaults, not explicitly required
- Cycling through presets, with reverse
- Message groups - a single named entity for a block of related messages
- next/previous page, and jump to bank messages
## [0.3.1] - 2024-11-5
- Major refactor.
- Intuitive is now based on use cases, not many features
- Simple is now a human-readable version of the backup file
- Renamed JsonGrammar to Grammar, NFC
- Renamed base/grammar to backup, NFC
- Renamed intuitive to simple, NFC
- Config mode is mostly complete

## [0.3.0] - 2024-09-22
- Removed a lot of functionality from Intuitive mode. It now corresponds much more closely to the backup config
- Created a new Config mode, a completely re-thought-out version of the old Intuitive mode
- Intuitive mode is still bidirectional with backup config, this is much more useful as it is closer to a 1-1 correspondence
- The new config mode is unidirectional - it maps to the intuitive mode

## [0.2.1] - 2024-09-22
- Bugfix: prev/next buttons not operating properly in navigator mode

## [0.2.0] - 2024-06-16
- Added get/set var methods to JsonGrammarModel
- Changed dict keys so that on complete models, a key can be marked as not required
    - This allows the setlist program output to be parsed
    - It doesn't include the controller settings
- Added per-key models to switch dicts
- add To Message Scroll to the Preset Array schema (MC6Pro Config)
- Added shifted name color and to msg scroll to preset
- Added Exp Preset Array
- Better handling of Intuitive messages, using first class functions
- All message types are now handled, more or less
- Added better 'required' parameter to dict keys
- Added 'per switch' models to switch dicts

## [0.1.2] - 2024-04-17
- Added names to all grammar nodes
- Added print_grammar program
- Refactored navigator mode, no functional change
- Improved error handling
- Made Jump Bank message have page default to 0
- Added "One Button" mode to Navigator Mode
- Added Navigator Mode override to mc6pro.py for testing
- Improved parsing to handle setlist files as well as backup files

## [0.1.1] - 2024-03-29
  
- Added Toggle Group
- Improved error messages
- Added versions to sample files
- Better versioning
- Fixed bug: bank messages not being converted to Base

## [0.1.0] - 2024-03-17
  
- Initial version with a change log
- Bank Messages
- Implementation.md a matrix describing which features are implemented
- renamed Bank to_description to display_description
- renamed Preset to_toggle to toggle_mode
- major refactor of grammar code: cleaned up tests, grammar nodes are python objects instead of dictionaries
- Added versioning
