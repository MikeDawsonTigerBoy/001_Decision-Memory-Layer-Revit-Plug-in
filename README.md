# 001 Decision Memory Layer

A record of why design decisions were made on long building projects, kept next to the work itself. It works the way commit history works for code, but for architecture.

> **Draft for review.** Lines tagged *(proposed)* are Claude's suggestions, not yet agreed. Section 10 lists the questions to settle before building.

## Status

An earlier web prototype exists, the Decision Timeline at decision-context-prototype.netlify.app, along with a Figma prototype. This repo is empty so far.

## 1. Problem statement

Building projects run for years and pass through many hands. The reasoning behind a decision ends up spread across emails, meeting minutes and people's memories: why a material was chosen, why an option was dropped, what the client agreed. When someone leaves, a client asks a question or a dispute comes up, teams re-argue settled decisions, repeat analysis or can't defend what was agreed.

## 2. Target audience

- **Primary:** architects and project leads on multi-year projects.
- **Secondary** *(proposed)*: BIM managers, client-side project managers, and anyone joining a project partway through.

## 3. Value proposition

Ask "why is it like this?" and get the answer in seconds. You see the decision, the options that were considered, who made it and when, all linked to the part of the model it affects.

## 4. Core functionality

*(proposed for v1)*
- Log a decision with: what was decided, why, the options considered, who decided, the date and the source (a meeting or an email).
- A timeline view of decisions across the project.
- Search and filter by building element, discipline or stage.
- Link a decision to a Revit element, view or sheet.

## 5. Key user journeys

1. **Capture:** after a design meeting, the project lead logs three decisions in under two minutes.
2. **Recall:** the client queries a façade change, so the architect selects the façade element and sees the full history of decisions on it.
3. **Handover:** a new team member reads through the decision timeline on their first day.

## 6. Non-goals

*(proposed)*
- Not a replacement for document control (Aconex, ACC), RFIs or issue tracking.
- Not a meeting-minutes tool.
- Not a contract or claims system.

## 7. Feasibility

- A web app version is straightforward.
- A Revit add-in means C#/.NET, Windows only, and the Revit API.
- A mobile app (the portfolio default) can't run inside Revit.

## 8. Assumptions and risks

- **Biggest risk:** people won't log decisions. If capturing a decision takes effort, the log stays empty, as minutes often do.
- **Assumption:** firms want this history kept. Some may prefer fewer written records because of liability.
- **Risk:** it overlaps with what Autodesk Construction Cloud already does.

## 9. Success metrics

*(proposed)*
- Decisions logged per active project each week.
- The share of "why" questions answered from the log rather than from email searches.
- Time to answer a "why" question, measured before and after.

## 10. Open questions and challenges

1. **What is it: a Revit plug-in, a web app or a phone app?**
   - The repo name says Revit plug-in, the portfolio lists it as a phone app (Expo), and the existing prototype is a website.
   - These are three different products, and settling this first avoids building the wrong one.
2. **How do decisions get in with almost no effort?**
   - The strongest AI angle is to pull candidate decisions out of meeting transcripts or email threads for a person to confirm, rather than asking people to type them in.
   - This is the core of the product, not an extra feature.
3. **Who pays, and who benefits?**
   - The person logging (the architect) isn't always the person who benefits later (the firm, the client, a lawyer). How does the capturer get value at the moment they log?
4. **Why not Autodesk Construction Cloud Issues or a shared spreadsheet?** What does this do that those can't?
5. **Is it the centrepiece?** As the main piece in Mike's PM positioning, which one claim should this case study prove?

## 11. Tech approach

To be decided, depending on the answer to question 1. Starting from a web prototype is fastest; the Revit add-in would come later.

## 12. Roadmap

- **v0 (done):** Netlify prototype and Figma prototype.
- **v1:** decide the format, then build the capture and recall flows.
- **Later:** a Revit add-in and AI extraction of decisions from meetings and email.
