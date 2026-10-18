# 001 Decision Memory Layer

A Revit plug-in connected to a web app. It records why major design decisions were made, linked to model elements and Design Options. It works the way commit history works for code, but for architecture.

> **Draft for review.** Lines tagged *(proposed)* are Claude's suggestions, not yet agreed. Section 10 lists the questions to settle before building.

## Status

- **Focus: active.** This is one of three featured prototypes, alongside 002 and 004.
- An earlier web prototype exists, the Decision Timeline at decision-context-prototype.netlify.app, along with a Figma prototype.
- **Code: none in this repo yet.**

## 1. Problem statement

Building projects run for years and change hands. Projects stop and restart: one might sit frozen for two years, then come back to life with a new director and a new production team. The reasoning behind the current design is spread across emails, minutes and the memories of people who have since left.

The new team has to retrace the decision tree to understand why the design looks the way it does. That's slow and expensive, and it risks undoing decisions that were made for good reasons.

## 2. Target audience

- **Primary:** directors, project architects and production teams who join, inherit or restart a long-running project.
- **Secondary:** BIM managers and client-side project managers.

## 3. Value proposition

Open the model, select an element and see why it is the way it is: the decision, the options that were rejected, who decided and when. No retracing needed.

## 4. Core functionality

**Revit plug-in**
- Record a major decision while working in the model.
- Link each decision to element IDs and to Design Options.
- See the history of decisions on any selected element.

**Web app**
- A timeline of decisions across the project.
- Search and filter.
- Read access for people who don't use Revit.

**Each decision record holds:** what was decided, why, the options considered, who decided, the date, and the source (a meeting, an email or a client instruction).

**What gets logged:** major decisions only. The aim is to capture the turning points, not every change. Revit already tracks file changes; this records the reasoning behind them.

## 5. Key user journeys

1. **Restart:** a project comes back after two years. The new director opens the web timeline and understands the 12 key decisions behind the current design in an hour.
2. **Join:** a new team member selects the façade in Revit and sees why it's built the way it is.
3. **Capture:** after a client meeting, the project architect logs a decision in Revit and links it to the affected elements and Design Option.

## 6. Non-goals

*(proposed)*
- Not a replacement for document control (Aconex, ACC), RFIs or issue tracking.
- Not a log of every change.
- Not a contract or claims system.
- Medical, legal and finance are out of scope for v1.

## 7. Feasibility

- **Revit add-in:**
  - It's built in C#/.NET on Windows using the Revit API.
  - The API exposes element IDs and Design Options.
  - The add-in should link decisions to each element's `UniqueId`, not its `ElementId`. The ElementId can change when models are worked on in parallel or copied; the UniqueId stays stable.
- **Web app:** straightforward to build. It needs a small backend so the Revit add-in and the web app share the same data.
- **Mike's strength:** he has used Revit daily for a decade and has real projects to test against.

## 8. Assumptions and risks

- **Biggest risk:** people won't log decisions. If capturing a decision takes effort, the log stays empty, as minutes often do.
- **Assumption:** firms want this history written down. Some may prefer fewer written records because of liability.
- **Overlap:** Autodesk Construction Cloud partly covers similar ground.
- **Model changes:** when elements are deleted or replaced, their links break. Decisions need to survive the element they were linked to.

## 9. Success metrics

*(proposed)*
- Time for a new team member to answer "why is it like this?", measured before and after.
- Decisions logged per active project each month.
- The share of decisions still linked to a valid element after 6 months of model changes.

## 10. Open questions and challenges

1. **How do decisions get in with almost no effort?**
   - The strongest AI angle is to suggest candidate decisions from meeting notes, emails or large model changes for a person to confirm.
   - Without this, the product relies on discipline that busy teams don't have.
2. **What counts as "major"?** A clear rule decides whether the log is useful or noisy. For example: anything signed off by the client, anything that changes cost, or anything that closes off an option.
3. **Who benefits at the moment of logging?** The architect who logs the decision rarely benefits later. What's in it for them today? For example, a quick record that covers them if the client queries it.
4. **Which comes first, the plug-in or the web app?** A web-only v1 with element IDs pasted in by hand would test the idea in days rather than weeks.
5. **Other domains (medical, legal, financial) are a strong part of the pitch,** for example "Why was a portfolio rebalanced?" Keep them as the vision, not the v1 scope. Each one is regulated and has its own tools and buyers.

## 11. Tech approach

- **Revit add-in:** C#/.NET, Revit API, Windows.
- **Web app:** React, with a shared backend API and database.
- **Portfolio:** the web app runs in the phone frames, and the Revit side gets a video demo.

## 12. Roadmap

- **v0 (done):** Netlify prototype and Figma prototype.
- **v1:** web app with manual element IDs, plus capture and recall flows.
- **v2:** Revit add-in that links to `UniqueId` and Design Options.
- **Later:** AI suggestions for decisions, then other domains.
