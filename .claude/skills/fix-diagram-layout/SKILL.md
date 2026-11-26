---
name: fix-diagram-layout
description: Improve the layout of one Excalidraw diagram (.excalidraw file) without changing what it says. Writes the result to a separate file for review and replaces the original only after the user approves. Use only when the user calls /fix-diagram-layout with a file path.
argument-hint: <path/to/diagram.excalidraw>
disable-model-invocation: true
---

# Fix diagram layout

Diagram to fix: `$ARGUMENTS`

Diagrams drawn by hand are rarely laid out well. Your job is to fix the layout:
where elements sit on the canvas and how lines and arrows run between them.
Nothing the diagram says may change.

## Permission to write files

This repository's `CLAUDE.md` says Claude must not create, edit or delete files
unless the user asks in that message. This skill is an explicit exception:

- Calling this skill is permission to create the review file (see below) and to
  change it while the user gives feedback.
- The user's approval of the result is permission to overwrite the original
  file and delete the review file.

Do not touch any other file in the repository. Throwaway helper scripts, if
you write any, go in your scratchpad directory, never in the repository.

## Goal

A layout the user finds easy to read:

- Elements are aligned horizontally and vertically.
- Lines and arrows do not cross. Where a crossing cannot be avoided, keep the
  number of crossings low and tell the user where they are.
- The reading order is natural: related elements sit close together and the
  diagram reads top to bottom or left to right.

You may rearrange the whole diagram. The original placement carries no meaning.
The method is up to you.

## What must not change

The content of the diagram stays exactly the same:

- The set of elements: add none, delete none, and keep every `id`.
- All text (`text`, `originalText`), font sizes, colours and styles.
- What connects to what: every arrow starts and ends at the same element as
  before.
- What belongs to what. Watch for meaning that exists only as position:
  - Text that is not bound to a container (no `containerId`) belongs to the
    shape it sits inside, e.g. attribute and method text inside a class box,
    or the divider line under a class name. Move it together with that shape
    and keep it inside.
  - Elements that share a `groupIds` entry move together as one unit.
  - Elements inside a frame (`frameId`) stay inside that frame.

One exception to "styles": **connector style is part of the layout.** Every line
and arrow in the diagram, including arrows that point from a note, uses the same
corner style: sharp, round or elbow. Use the style most connectors already have.
Change a connector that differs to match, and say so in the report. Only the
corner style changes (`roundness`, `elbowed`). Arrowheads, stroke and colour
stay as they are, because in diagrams such as UML they carry meaning. When a
connector ends up sharp or round, remove leftover elbow-mode fields
(`fixedSegments`, `startIsSpecial`, `endIsSpecial`), because Excalidraw may still
draw it differently.

You may change geometry: `x`, `y`, `width`, `height`, `points`, and the
binding details that follow from moving shapes (`startBinding`, `endBinding`,
`boundElements`). Keep these consistent:

- `points` of lines and arrows are relative to the element's `x`, `y`.
- A shape's `boundElements` and the arrow's `startBinding` / `endBinding` must
  refer to each other. After moving a shape, its bound arrows must still meet it.
- Bound text (`containerId` set) stays centred in its container.
- For every element you change, increase `version` and set a new random
  `versionNonce`, so Excalidraw picks up the change.

## Steps

1. Read the file. If it is mostly freehand strokes or images rather than shapes,
   text, lines and arrows, tell the user this skill is not meant for it and stop.
2. Work out the new layout.
3. Write the result next to the original as `<name>.layout.excalidraw`, e.g.
   `class_diagram.excalidraw` → `class_diagram.layout.excalidraw`. Never write to
   the original file at this point.
4. Report back (see below) and ask the user to review the review file.
5. When the user names layout problems, fix them in the review file and report
   again. Repeat until the user approves or stops.
6. On approval, copy the review file over the original and delete the review file.
   Confirm both in one line.

## Report

Keep it short and easy to scan:

- **Done:** where the review file is, and what you changed in a few bullets.
- **Crossings left:** where, and why they could not be removed (omit if none).
- **Connector style:** which connectors you changed to match the rest, and to
  which style (omit if none).
- **Questions:** anything you could not decide, e.g. which shape a loose text
  belongs to (omit if none).
- **Suggestions:** what looks wrong, missing or incomplete in the diagram's
  content, e.g. a `TODO` placeholder, a class without attributes, an arrow
  without a label. Point it out only; never fix content yourself.
