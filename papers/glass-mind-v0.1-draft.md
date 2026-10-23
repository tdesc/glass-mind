# Glass Mind: The Operational Self-Model

**A provenance-grounded architecture for agents that can observe, attribute, explain, and revise their own causal behavior**

**Open paper · working draft 0.1 · August 2026**
**Valentin Kalinin · mind.glass / Colony**

> **Claim ceiling:** operational self-model and causal self-observation — not phenomenal consciousness, not an ARC-AGI-3 solve claim, and not evidence of autonomous general intelligence.

## Abstract

Contemporary agents can emit traces, narrate their actions, and preserve episodic memory. None of those capabilities, by itself, constitutes a reliable self-model. A trace can show that a tool call occurred without recording what the agent expected. A narrative can explain an outcome after it is known. A memory can preserve a mistake without preserving the conditions under which the mistake was made. And an observer can become dangerous if observation silently turns into authority.

Glass Mind is an architecture for an **operational self-model**: a source-attributed, temporally ordered representation of an agent’s own causal process. Before an action, the system seals what it expects and why. A separate authority layer decides whether one bounded intervention may occur. The execution substrate records what the body actually did. A sealed afterstate closes the interaction with reality. The system then distinguishes three questions that are often conflated: whether the action produced the predicted dynamics, whether the result advanced the current goal, and whether a terminal condition was reached. A revision receipt records what changed in the internal model. Natural-language self-report is generated only as a projection of the same evidence.

This design does not claim consciousness. It makes a narrower and falsifiable claim: an agent can be engineered so that it cannot silently rewrite its pre-action expectation, cannot confuse a world-model contradiction with a broken self-observation record, and cannot acquire motor authority merely by becoming more observant. Early ARC-AGI-3 experiments show complete action-to-afterstate closure and narrow causal attribution from a synthesized option through Planner and Critic to an executed action. They do not yet demonstrate typed goal awareness, autonomous cross-session improvement, or general transfer.

The next research step is to make small program synthesis a native mode of thought. Glass Mind should not merely report what happened. A Self Capability Model should compile a bounded program, simulate it under competing world models in a **lucid dream**, execute one admitted step, wake on the real afterstate, and recompile. Dreams may propose programs. Only reality may create evidence.

---

## 1. The problem: traces are not a self-model

Agent systems increasingly expose spans, tool logs, memory records, and verbal reflections. These are valuable, but they answer different questions.

- **Telemetry** asks: what code path ran?
- **Provenance** asks: which entities, activities, and agents produced this artifact?
- **Reflection** asks: what interpretation should be carried into the next attempt?
- **A self-model** must additionally ask: what did the system expect before acting, what action was actually authorized and executed, what changed in the world, where did the prediction fail, and what in the system changed as a consequence?

The gap matters because a post-hoc explanation can be coherent while being causally false. A planner may say it selected candidate A while a fallback actually dispatched candidate B. A graph trace may show a `goal_reasoner` node without proving that the goal was correct. A voice may claim learning while the belief state did not change. A memory may record the same event through several projections and mistake repetition for independent confirmation.

Glass Mind treats these as engineering failures, not philosophical mysteries.

### 1.1 Four recurrent failure modes

**Post-hoc rationalization.** The system writes the forecast after seeing the outcome, creating an unfalsifiable story.

**Authority drift.** An observer, critic, or narrator gains the ability to alter candidate ordering or issue actions because it has access to more context.

**Evidence echo.** One causal event is copied into a graph, a voice message, and a memory record, then counted as several confirmations.

**Silent absence.** Missing evidence is replaced by a plausible default instead of being represented as `not_observed`.

The architecture below is designed to make each failure detectable.

---

## 2. Definition: an operational self-model

An operational self-model is a bounded model of the system’s own causal competence and behavior. It is not a scalar “awareness score,” an unfiltered chain of thought, or a narrative persona.

At causal turn \(t\), let:

- \(o_t\) be the observed state;
- \(b_t\) be the current belief state;
- \(f_t\) be a sealed forecast commitment;
- \(u_t\) be the selected semantic intervention;
- \(x_t\) be the execution receipt;
- \(o_{t+1}\) be the sealed afterstate;
- \(v_t\) be the dynamics, goal, and terminal verdicts;
- \(r_t\) be the internal revision;
- \(p_t\) be provenance and authority evidence.

The self-observation packet is a join over those records:

\[
S_t = J(f_t, u_t, x_t, o_{t+1}, v_t, r_t, p_t)
\]

The ordering is part of the claim:

\[
f_t \prec u_t \prec x_t \prec o_{t+1} \prec v_t \prec r_t
\]

A self-report is a projection of the packet:

\[
N_t = \Pi(S_t)
\]

It is not an independent source of evidence.

### 2.1 What the self-model must know

A mature Self Capability Model should represent:

\[
P(\text{outcome},\ \text{goal progress},\ \text{failure source}
\mid \text{semantic state},\ \text{option},\ \text{morphology},\
\text{representation hypothesis},\ \text{own version},\
\text{authority},\ \text{budget})
\]

This is a competence model, not a personality model. It answers:

- What program can I compile here?
- Under which role bindings and phase assumptions is it applicable?
- How uncertain am I about the predicted afterstate?
- Which component is most likely to fail: perception, role binding, dynamics, goal inference, planning, motor binding, or authority?
- What is the smallest intervention that would distinguish the leading models?
- When should I abstain?

---

## 3. Constitutional invariants

Glass Mind is organized around nine invariants.

### I. Expectation precedes action

A prediction, goal predicate, reason code, and falsifier are sealed before motor admission. They cannot be rewritten after the afterstate arrives.

### II. Observation does not imply authority

\[
\operatorname{observe}(S_t) \not\Rightarrow \operatorname{authorize}(u_t)
\]

Glass Mind, the graph observer, DecisionGraph, and voice remain advisory. Planner, Critic/NLA, and the execution substrate retain distinct responsibilities.

### III. One admission authorizes at most one intervention

A one-shot admission is tied to the current observation, candidate, source, session, episode, and action schema. Replay is rejected.

### IV. The body is the witness of action

“I did” is established by the execution substrate and SDK receipt, not by planner intent or graph telemetry.

### V. Reality outranks prediction

The sealed afterstate is authoritative about what occurred. It does not automatically determine what the occurrence means for the goal.

### VI. Contradiction is not inconsistency

A complete self-observation may correctly record that a prediction was wrong:

```yaml
observation_integrity: complete
world_model_verdict: contradicted
strategy_transition: cancel
```

`inconsistent` is reserved for conflicting receipts, option identifiers, causal times, source bindings, or lineage.

### VII. One causal root may have many projections

Graph telemetry, Glass Mind, NLA voice, and Dual Consciousness may render the same event differently, but they must refer to one causal root. Repeated projections are not independent evidence.

### VIII. Absence stays loud

Every semantic field is `observed`, `not_observed`, or `not_applicable`. Missing producers are named rather than inferred.

### IX. A dream may propose; only reality may confirm

Imagined rollouts can generate candidate programs, predictions, and discriminating probes. They cannot mint causal evidence, a terminal claim, or durable memory authority.

---

## 4. Architecture

Glass Mind separates four planes.

```text
CAUSAL EVIDENCE PLANE
observation → forecast → action receipt → sealed afterstate → verdict → revision

AUTHORITY PLANE
Planner → Critic / NLA → one-shot admission → body-specific materialization

REFLECTIVE PLANE
SelfObservationPacket → DecisionGraph → Glass Mind / Voice / Dual projections

LEARNING PLANE
Certified transition → SelfCapabilityModel → program synthesis → candidate option
```

The planes communicate through typed receipts. They do not share implicit authority.

### 4.1 Core records

#### SelfForecastCommitment — “I EXPECT”

Created before action:

```yaml
identity:
  brain_lineage_sha256:
  session_scope_sha256:
  episode_scope_sha256:
  own_causal_time:

observation:
  observation_sha256:
  semantic_state_sha256:
  belief_before_sha256:

intention:
  goal_hypothesis_sha256:
  mechanism_hypothesis_sha256:
  selected_candidate_sha256:

prediction:
  expected_effect:
  predicted_outcomes_ppm:
  expected_progress_predicate:
  falsifier:
```

#### SelfActionReceipt — “I DO”

Created by the execution boundary:

```yaml
commitment_sha256:
critic_attestation_sha256:
motor_admission_nonce_sha256:
requested_action_sha256:
accepted_action_sha256:
sdk_call_id:
runtime_accepted:
```

#### SelfAfterstateClosure — “I OBSERVE”

```yaml
sealed_afterstate_sha256:
semantic_delta_sha256:
verdicts:
  dynamics: supported | contradicted | inconclusive | parse_failure
  goal: progress | neutral | regress | unknown
  terminal: satisfied | unsatisfied | unknown
```

#### SelfRevisionReceipt — “I REVISE”

```yaml
belief_before_sha256:
belief_after_sha256:
hypothesis_changes:
posterior_deltas_ppm:
program_decision: continue | cancel | rebind | abstain | stop
memory_candidate: none | soft | hard | quarantine
```

#### SelfObservationPacket — “I CAN ACCOUNT FOR THIS TURN”

The packet is a materialized view over primary evidence. It does not infer missing facts and does not authorize action.

### 4.2 Graph-bound causal identity

A single embodied turn may traverse multiple graph nodes and branches. Therefore the join is not:

```text
ARC turn ↔ one graph node
```

It is:

```text
ARC causal turn
↔ bounded graph trace segment
↔ selected branch + abandoned branches
↔ one admitted action
↔ one sealed afterstate
```

The join uses explicit decision identity, causal time, source binding, and lineage — never timestamp proximity alone.

### 4.3 DecisionGraph

DecisionGraph records whether an internal construction actually changed the decision:

```text
synthesized option
→ candidate set changed
→ ranking changed
→ Planner selected the option
→ Critic reviewed the same option ID
→ CompetitionKernel executed the bound action
→ a sealed afterstate followed
```

Its mode must be explicit:

```yaml
decision_graph_mode: observer_shadow
option_planner_mode: active
execution_owner: competition_kernel
observer_motor_authority: false
```

The observer attributes causality; it does not create or execute the action.

---

## 5. Three verdict axes

A central contribution of Glass Mind is the separation of three questions.

### 5.1 Observation integrity

Did the self-model join the correct records?

```text
complete | partial | inconsistent | not_observed
```

### 5.2 World-model verdict

Did the observed dynamics match the pre-action prediction?

```text
supported | contradicted | inconclusive | parse_failure | not_evaluated
```

### 5.3 Strategy transition

What happened to the current option or program?

```text
continue | cancel | rebind | revise | abstain | stop | not_applicable
```

Goal and terminal verdicts remain separate. An action can produce a correctly predicted structural change while making no progress toward the goal. A world-model contradiction can be observed with perfect integrity. A level can remain unfinished even when local dynamics are supported.

This separation prevents a common failure: treating “something changed” as “the task improved.”

---

## 6. From self-observation to native program synthesis

A self-model that only reports what happened may become an excellent narrator without becoming a better problem solver. The next organ is a small, typed program synthesizer that uses the Self Capability Model as its native language of thought.

### 6.1 Why small program synthesis

Internal analysis of successful specialized ARC solvers suggests a recurring structure:

```text
frame
→ semantic roles
→ explicit state and transition law
→ exact goal predicate
→ executable program
→ one motor step
→ fresh afterstate
→ recompile / falsify / block
```

Their advantage was not a richer monologue. It was a compact causal compiler with task algebra, role binding, a goal predicate, an executable program, termination, and decision precedence when the compiled program was valid.

The universal architecture should preserve those strengths without routing by environment identity or copying historical routes.

### 6.2 MechanismInstance

```yaml
MechanismInstance:
  family:
  current_role_bindings:
  state_variables:
  phase_hypotheses:
  competing_transition_models:
  invariants:
  applicable_algebras:
  candidate_goals:
  evidence_refs:
```

### 6.3 SemanticOption

A synthesized option is a bounded program with an initiation set, internal policy, and termination conditions:

```yaml
SemanticOption:
  initiation:
    phase_predicates:
    role_binding_predicates:
    confidence_floor:

  program:
    typed_steps:

  per_step:
    predicted_outcomes:
    expected_progress_predicate:
    falsifier:

  termination:
    success_predicate:
    contradiction_predicate:
    ood_predicate:
    max_steps:
    max_replans:

  recovery:
    rebind | recompile | probe | abstain
```

A valid option may receive Planner precedence over generic novelty spray only when applicability, current role binding, goal predicate, falsifier, competence floor, OOD threshold, Critic acceptance, and one-step execution are all satisfied.

---

## 7. Lucid dreaming

Glass Mind’s “dreaming” is not an ungrounded narrative and not an alternative source of truth. It is a sandbox for program simulation under explicit uncertainty.

### 7.1 The lucid distinction

A lucid dream knows that it is imagined:

```yaml
DreamTrace:
  epistemic_status: imagined_only
  causal_evidence: false
  source_observation_sha256:
  world_model_versions:
  goal_hypothesis:
  program_ast:
  assumptions:
  competing_models:
  predicted_trajectory:
  uncertainty:
  expected_goal_delta:
  first_uncertain_step:
  falsifiers:
```

It may produce:

- a candidate program;
- a counterfactual prediction;
- a discriminating probe;
- a risk estimate;
- a reason to abstain.

It may not produce:

- a confirmed transition;
- a terminal claim;
- durable causal evidence;
- motor authority.

### 7.2 Dream long; execute one

The system may imagine four to eight steps but executes one:

```text
dream horizon = 4–8
execution horizon = 1
```

After each real afterstate, the remaining program is recompiled from the fresh frame. This guards against planner exploitation of an imperfect model.

### 7.3 Competing dreams

The system should not imagine one cinematic future. It should preserve several credible mechanism models:

```yaml
DreamRollout:
  program_id:
  branches:
    - model_id: H1
      probability_ppm:
      states:
      goal_result:
    - model_id: H2
      probability_ppm:
      states:
      goal_result:
  first_disagreement:
  safest_real_probe:
```

When credible models agree, the first program step may be proposed. When they disagree, the system chooses the smallest safe probe that most changes the posterior.

---

## 8. Operational awareness maturity

Glass Mind avoids arbitrary percentages and uses a falsifiable ladder.

| Level | Capability | Current evidence status |
|---|---|---|
| C0 | Observe own action and sealed afterstate | Verified in bounded ARC runs |
| C1 | Detect contradiction, no-op, and local discrepancy | Verified |
| C2 | Revise a current-episode hypothesis and cancel stale strategy | Narrowly verified |
| C3 | Compile self-observation into a Planner-consumed, goal-bound option | Frontier |
| C4 | Preserve semantic learning across a real restart without source edits | Not demonstrated in the ten-session wave |
| C5 | Improve autonomously across sessions and transfer to a new morphology | Not demonstrated |
| C6 | Open-ended cross-domain general intelligence | Not claimed |

The nearest achievable milestone is C3: a synthesized option with an immutable `expected_progress_predicate`, consumed by Planner and Critic, executed one step, and revised from a sealed afterstate.

---

## 9. Internal evidence and its limits

The evidence in this section is project-internal and source-bound. It is not an independent benchmark audit.

### 9.1 Ten-session self-observation audit

Across sessions A1065-v5 through A1074, the system reported:

- 5,470 sealed causal events;
- 374 closed turns;
- 368 real environment actions;
- 368 prediction tickets, 368 SDK calls, and 368 sealed afterstates;
- zero invalid motor actions, hidden retries, or terminal resets;
- one distinct solved level: ar25 L1.

Every session used `durable_memory.mode=start_clean`. Therefore wave-to-wave improvement came from source changes between runs, not from autonomous cross-session learning. This is a crucial negative result: strong self-observation was demonstrated, but persistent self-teaching was not.

### 9.2 ADR-298 DecisionGraph milestone

A later eight-action dc22 experiment tested a narrower claim: `causal_decision_projection_not_execution`.

- Baseline b1: 0/8 complete projections.
- Candidate b3: 3/8 complete projections.
- Turns 5–7 attributed a changed candidate set, ranking, and action to a `synthesized_option` shared by Planner and Critic.
- All eight turns preserved prediction/SDK/sealed-afterstate parity.
- The observer had no Planner or motor authority and did not call the SDK.
- A contradiction canceled the stale option tail.

The experiment did not solve a level and did not demonstrate goal progress. It exposed an important schema error: `afterstate_contradicted` was initially classified as self-observation `inconsistent`. The correct semantics are:

```yaml
observation_integrity: complete
world_model_verdict: contradicted
strategy_transition: cancel
```

This correction illustrates the purpose of Glass Mind: the architecture must distinguish “I observed myself incorrectly” from “I correctly observed that I was wrong.”

---

## 10. Evaluation protocol

A self-model is useful only if it changes measurable cognition without corrupting authority or evidence.

### 10.1 Core metrics

```yaml
causal_closure:
  sdk_calls_with_prediction_and_sealed_afterstate:

attribution_coverage:
  actions_with_planner_critic_execution_lineage:

forecast_integrity:
  posthoc_forecast_mutations:

self_report_grounding:
  claims_with_exact_packet_fields_and_evidence_refs:

revision_yield:
  contradictions_that_change_model_or_candidate_set:

planner_consumption:
  synthesized_options_that_enter_and_change_selection:

goal_predicate_coverage:
  option_steps_with_pre_action_typed_progress_predicate:

restart_learning_delta:
  same_source_clean_vs_hydrated_decision_difference:

ood_behavior:
  calibrated_reuse | probe | abstain:
```

### 10.2 Required controls

**Observer parity.** Observer enabled and disabled must produce identical candidate and action digests.

**Memory-only baseline.** A complex self-model must outperform direct empirical memory on solve rate, efficiency, calibration, abstention, or transfer.

**Option-off ablation.** Removing the synthesized option must cause a bounded target loss without technical failure.

**Source-identical restart pair.** Cross-session learning is claimed only when source, policy, image, seed, order, and budgets remain identical.

**Morphology counterexample.** The same appearance with a different mechanic must be rejected; a mechanic-preserving transformation should yield an equivalent option.

**Evidence ancestry.** Derived projections cannot confirm their own causal ancestor.

### 10.3 Failure states

Glass Mind should name operational pathologies:

- **Asystole:** no next admissible step and no typed stop.
- **Tachycardia:** many actions without model revision.
- **Arrhythmia:** a semantic cycle repeats without new utility.
- **Fibrillation:** several components act as decision owner.
- **Ectopic beat:** an SDK action occurs outside the current admission.
- **Ischemia:** a prediction exists but no sealed afterstate returns.
- **Autoimmune memory:** an old scar blocks a newly relevant context.

These names are diagnostic metaphors, not biological claims.

---

## 11. Relationship to prior work

Glass Mind combines several established research lines but makes a different systems claim.

### Continuous self-modeling

Bongard, Zykov, and Lipson demonstrated a robot that inferred its own structure from actuation–sensation relationships, used the self-model to generate locomotion, and adapted after damage. Glass Mind shares the emphasis on self-model revision through action-conditioned evidence, but extends it with provenance, explicit authority, typed goal verdicts, and evidence-grounded self-report.

### Active self and sense of control

Kahl and colleagues proposed an embodied active-self architecture that combines bottom-up sensorimotor adaptation with top-down strategy selection. Glass Mind operationalizes a related question as a receipt-backed estimate of control: did the admitted action cause the observed effect, and did the effect advance the declared goal?

### Provenance and tracing

W3C PROV provides a domain-agnostic model of entities, activities, agents, derivations, and provenance bundles. OpenTelemetry provides traces, spans, context, events, links, and status. Glass Mind uses those ideas as substrate, then adds epistemic semantics that generic tracing does not provide: pre-action forecast, falsifier, dynamics/goal/terminal verdicts, revision, and claim ceiling.

### Verbal reflection

Reflexion shows that language agents can improve by storing verbal feedback in episodic memory. Glass Mind adopts the value of reflection while imposing a stronger temporal rule: narrative cannot retroactively become the forecast that preceded the action.

### Object-centric world models

C-SWM and Slot Attention motivate object- and relation-centric state representations. Glass Mind keeps deterministic components and competing role hypotheses as witnesses rather than making a learned slot model the sole source of truth.

### Dynamics and goal factorization

Successor Features separate environment dynamics from reward or task value. Glass Mind adopts the architectural factorization without assuming that ARC tasks share identical dynamics: `dynamics supported` and `goal progress` are separate verdicts.

### Temporal abstraction

Option-Critic formalizes options through initiation, internal policy, and termination. Glass Mind uses that contract for typed symbolic options, whether or not they are learned by gradient descent.

### Epistemic exploration

Plan2Explore selects actions for expected future novelty using a world model. Glass Mind similarly requires probes to distinguish explicit competing models; simple action-count novelty is not treated as information gain.

### Program-learning and dreaming

DreamCoder alternates program solving with wake–sleep abstraction. Glass Mind adopts the idea of a growing language of thought, while refusing to count dreamed or replayed examples as independent causal evidence.

---

## 12. Threats to validity

### The observer may alter the observed system

Latency, memory pressure, scheduling, or nondeterministic iteration can change decisions even without explicit authority. Observer-on/off parity is therefore a permanent gate.

### Source edits can masquerade as self-improvement

Improvements across sessions do not demonstrate learning when the code changed between runs. Source-identical paired experiments are required.

### Self-report can create epistemic echo

The system must never treat its own explanation as independent support for the hypothesis being explained.

### Game identity can leak through structure

Removing a `game_id` field is insufficient if dimensions, palette, coordinates, or morphology form an implicit identifier. Cross-morphology and same-appearance/different-mechanic controls are required.

### Memory can become autoimmune

Durable contradictions require source, ontology, phase, goal, effect, and recovery scope. No-effect evidence should usually lower utility rather than create a permanent global block.

### Complete telemetry can preserve an incorrect ontology

A perfectly recorded wrong interpretation remains wrong. Glass Mind must preserve uncertainty, competing hypotheses, and falsifiers.

### “Operational self” can be mistaken for phenomenal consciousness

The architecture says nothing about subjective experience. It provides falsifiable evidence about observation, attribution, control, explanation, and revision.

---

## 13. Research roadmap

### Phase A — One self, one causal turn

Join ARC causal time, graph run identity, Planner, Critic, action, and sealed afterstate into one source-attributed event.

### Phase B — Goal-bound option

Compile one verified transition motif into a Planner-consumed SemanticOption with a pre-action `expected_progress_predicate` and per-step falsifier.

### Phase C — One lucid embodied step

Dream several branches, execute one admitted step, and recompile from the real afterstate.

### Phase D — Restart-stable competence

Persist source- and ontology-bound semantic learning; prove that a fresh process changes its decision without source edits and without overblocking adjacent hypotheses.

### Phase E — Cross-morphology competence envelope

Reuse, compose, probe, or abstain on a new morphology. Compare against direct empirical memory and option-off controls.

### Phase F — Bounded scientific intelligence

Maintain competing causal models, choose discriminating experiments, grow a reusable DSL, and transfer verified mechanisms within a bounded domain.

This final phase would be a meaningful form of autonomous scientific intelligence inside ARC-like worlds. It would still not establish open-ended AGI or consciousness.

---

## 14. Conclusion

Glass Mind begins with a modest claim: an agent should be able to prove what it expected, what it selected, what its body did, what reality returned, where the model failed, what changed internally, and what it did not observe.

That claim leads to a strict architecture:

```text
I EXPECT  — sealed before action
I CHOOSE  — attributed to Planner and Critic
I DO      — witnessed by the execution substrate
I OBSERVE — closed by a sealed afterstate
I REVISE  — evidenced by a changed belief or strategy
I TALK    — projected from the same causal record
```

The system does not become more authoritative merely by becoming more self-aware. The observer remains an observer. The narrator remains a narrator. The world remains the final witness of what happened.

The next step is not more introspection. It is one observation becoming a better program: a small, falsifiable option compiled from current roles and mechanism hypotheses, dreamed under uncertainty, executed one step, and revised by reality.

> **Glass Mind does not claim that a machine is conscious. It proves when, how, and to what extent an agent can observe, attribute, explain, and revise its own causal behavior.**

---

## References

1. Bongard, J., Zykov, V., & Lipson, H. (2006). *Resilient Machines Through Continuous Self-Modeling*. Science 314(5802), 1118–1121. DOI: 10.1126/science.1133687.
2. Kahl, S., Wiese, S., Russwinkel, N., & Kopp, S. (2021). *Towards autonomous artificial agents with an active self: modeling sense of control in situated action*. arXiv:2112.05577.
3. W3C. (2013). *PROV-DM: The PROV Data Model*.
4. OpenTelemetry. *Traces: spans, context, events, links, and status*.
5. Shinn, N. et al. (2023). *Reflexion: Language Agents with Verbal Reinforcement Learning*. arXiv:2303.11366.
6. Kipf, T., van der Pol, E., & Welling, M. (2019). *Contrastive Learning of Structured World Models*. arXiv:1911.12247.
7. Locatello, F. et al. (2020). *Object-Centric Learning with Slot Attention*. arXiv:2006.15055.
8. Barreto, A. et al. (2016). *Successor Features for Transfer in Reinforcement Learning*. arXiv:1606.05312.
9. Bacon, P.-L., Harb, J., & Precup, D. (2016). *The Option-Critic Architecture*. arXiv:1609.05140.
10. Sekar, R. et al. (2020). *Planning to Explore via Self-Supervised World Models*. arXiv:2005.05960.
11. Ellis, K. et al. (2020). *DreamCoder: Growing generalizable, interpretable knowledge with wake-sleep Bayesian program learning*. arXiv:2006.08381.
12. Kalinin, V. / Colony. (2026). *ADR-298: Semantic Assembly — Self-Observation Packet* and associated implementation notes, PRs #566–#569.

### Implementation notes

- PR #566 — evidence-bound SelfObservationPacket and loud absence.
- PR #567 — ARC causal event projection.
- PR #568 — GraphConsciousnessObserver identity join.
- PR #569 — evidence-bound NLA voice and DualSignature divergence.
- ADR-298 DecisionGraph internal verdict — narrow causal-decision attribution, not execution or solve authority.
