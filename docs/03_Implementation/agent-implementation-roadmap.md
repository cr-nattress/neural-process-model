---
title: Agent Implementation Roadmap (Node.js/TypeScript)
type: implementation
cognitive_function: meta
ai_mapping: implementation_plan
last_update: 2025-11-02
tags: [agents, typescript, implementation, roadmap]
---

# 🤖 Agent Implementation Roadmap

## Overview

This document outlines the first 10 agents to implement for CSAL, ordered from simplest to most complex. Each agent is designed for Node.js/TypeScript with minimal dependencies and maximum clarity.

**Implementation Philosophy:**
- Start simple, iterate to complexity
- Each agent is a standalone module
- Clear interfaces for composition
- Test-driven development
- Brain-inspired but pragmatic

---

## Agent 1: Pattern Recognition Agent 🔍

### Brain Analogy: Primary Visual Cortex (V1) / Sensory Processing

**Biological Basis:**
- **Location:** Occipital lobe (visual), temporal lobe (auditory), parietal (touch)
- **Function:** Detect basic features (edges, frequencies, textures)
- **Mechanism:** Hierarchical feature detection, receptive fields
- **Properties:**
  - Rapid, parallel processing
  - Bottom-up signal flow
  - Feature maps for different qualities (orientation, color, motion)
  - ~100-150ms processing time in humans

**Cognitive Process:**
The primary sensory cortices perform the first-pass analysis of incoming stimuli. V1 neurons, for example, respond to specific orientations of lines. This creates a feature map that higher cortical areas use for object recognition.

**Computational Essence:**
Simple pattern matching and feature extraction - finding recurring patterns in data streams.

### TypeScript Implementation

**Complexity:** ⭐ (Simplest)

**Core Functionality:**
- Detect patterns in text, numbers, or data streams
- Simple regex-based or substring matching
- Frequency analysis
- Basic classification

**Interface:**
```typescript
interface Pattern {
  id: string;
  pattern: string | RegExp;
  type: 'exact' | 'regex' | 'fuzzy';
  metadata?: Record<string, any>;
}

interface PatternMatch {
  pattern: Pattern;
  match: string;
  confidence: number;
  position?: number;
}

class PatternRecognitionAgent {
  private patterns: Map<string, Pattern>;

  constructor() {
    this.patterns = new Map();
  }

  // Register patterns to detect
  registerPattern(pattern: Pattern): void;

  // Scan input for known patterns
  recognize(input: string): PatternMatch[];

  // Learn new patterns from examples
  learnPattern(examples: string[], patternId: string): Pattern;

  // Get recognition statistics
  getStats(): { totalPatterns: number; matchRate: number };
}
```

**Dependencies:**
- None (pure TypeScript)

**Key Features:**
- Pattern registry
- Multiple matching strategies (exact, regex, fuzzy)
- Confidence scoring
- Simple learning from examples

**Test Cases:**
- Detect email patterns
- Identify phone numbers
- Recognize code patterns
- Find repeated phrases

---

## Agent 2: Attention Filter Agent 🎯

### Brain Analogy: Anterior Cingulate Cortex (ACC) / Salience Network

**Biological Basis:**
- **Location:** Medial frontal cortex, wraps around corpus callosum
- **Function:** Detect conflicts, allocate attention, filter stimuli by importance
- **Mechanism:**
  - Error detection and conflict monitoring
  - Salience computation (novelty, relevance, urgency)
  - Resource allocation to competing processes
  - Modulation of other brain regions
- **Properties:**
  - ~200-300ms for conflict detection
  - Integrates emotional and cognitive information
  - Connected to both DMN and ECN
  - High metabolic activity

**Cognitive Process:**
The ACC acts as a "cognitive alarm system." When you're reading and hear your name, the ACC detects this salient stimulus and redirects attention. It monitors for conflicts (Stroop task: word "RED" in blue ink) and signals when more cognitive control is needed.

**Neurotransmitters:** Dopamine (motivation), glutamate (excitation)

**Computational Essence:**
Filtering and prioritization - deciding what deserves processing resources.

### TypeScript Implementation

**Complexity:** ⭐⭐

**Core Functionality:**
- Score items by relevance to current goal
- Filter streams based on salience
- Priority queue management
- Resource allocation

**Interface:**
```typescript
interface AttentionItem<T = any> {
  id: string;
  data: T;
  priority: number;
  timestamp: Date;
  metadata?: {
    novelty?: number;
    relevance?: number;
    urgency?: number;
  };
}

interface AttentionContext {
  currentGoal?: string;
  activeTopics: string[];
  thresholds: {
    novelty: number;
    relevance: number;
    urgency: number;
  };
}

class AttentionFilterAgent<T = any> {
  private context: AttentionContext;
  private capacity: number = 7; // Miller's Law

  constructor(capacity?: number) {
    this.capacity = capacity || 7;
  }

  // Score item's salience based on context
  computeSalience(item: T, context: AttentionContext): number;

  // Filter items by attention threshold
  filter(items: AttentionItem<T>[]): AttentionItem<T>[];

  // Update attention context (what matters now)
  updateContext(context: Partial<AttentionContext>): void;

  // Detect conflicts (competing high-priority items)
  detectConflict(items: AttentionItem<T>[]): boolean;

  // Get top N items within capacity
  getTopItems(items: AttentionItem<T>[], n?: number): AttentionItem<T>[];
}
```

**Dependencies:**
- None (pure TypeScript)

**Key Features:**
- Multi-factor salience scoring (novelty, relevance, urgency)
- Capacity constraints (7±2 items)
- Context-aware filtering
- Conflict detection

**Test Cases:**
- Filter 100 messages to top 7 most important
- Detect when two urgent items compete
- Adapt filtering based on goal changes
- Handle novelty decay over time

---

## Agent 3: Working Memory Agent 🧮

### Brain Analogy: Dorsolateral Prefrontal Cortex (dlPFC)

**Biological Basis:**
- **Location:** Lateral surface of frontal lobe (Brodmann areas 9, 46)
- **Function:** Temporary storage and manipulation of information
- **Mechanism:**
  - Sustained neural firing maintains information
  - ~7±2 items capacity (Miller's Law)
  - Active maintenance through rehearsal
  - Vulnerable to interference and decay
- **Properties:**
  - 15-30 second duration without rehearsal
  - Integrates with attention and executive control
  - Essential for reasoning and comprehension
  - High energy cost to maintain

**Cognitive Process:**
Working memory is your "mental workspace." When you do mental math (23 + 47), you hold the numbers and intermediate results in working memory. When you follow directions ("turn left, then right at the third light"), you're using working memory. It's like RAM in a computer - fast, limited, and volatile.

**Neurotransmitters:** Dopamine (D1 receptors critical for maintenance)

**Capacity Limitations:**
- **Span:** 7±2 chunks for simple items, 4±1 for complex items
- **Decay:** ~2 seconds per item without rehearsal
- **Interference:** New items can displace old ones

**Computational Essence:**
A constrained, fast-access cache with intelligent eviction.

### TypeScript Implementation

**Complexity:** ⭐⭐

**Core Functionality:**
- Store items temporarily with capacity limits
- LRU or priority-based eviction
- Decay mechanism (TTL)
- Rehearsal to prevent decay

**Interface:**
```typescript
interface WorkingMemoryItem<T = any> {
  id: string;
  content: T;
  priority: number;
  createdAt: Date;
  lastAccessed: Date;
  rehearsalCount: number;
  ttl?: number; // time-to-live in ms
}

interface WorkingMemoryStats {
  capacity: number;
  currentSize: number;
  totalAccesses: number;
  evictionCount: number;
  averageItemLifetime: number;
}

class WorkingMemoryAgent<T = any> {
  private items: Map<string, WorkingMemoryItem<T>>;
  private capacity: number;
  private defaultTTL: number;

  constructor(capacity: number = 7, defaultTTL: number = 30000) {
    this.capacity = capacity;
    this.defaultTTL = defaultTTL;
    this.items = new Map();
  }

  // Add item to working memory
  add(id: string, content: T, priority?: number, ttl?: number): boolean;

  // Retrieve item (updates lastAccessed)
  get(id: string): WorkingMemoryItem<T> | undefined;

  // Rehearse item to prevent decay
  rehearse(id: string): boolean;

  // Remove item explicitly
  remove(id: string): boolean;

  // Check if capacity is available
  hasCapacity(): boolean;

  // Get all current items
  getAll(): WorkingMemoryItem<T>[];

  // Force eviction of least important item
  evict(): string | null;

  // Clean up expired items
  cleanup(): number;

  // Get statistics
  getStats(): WorkingMemoryStats;
}
```

**Dependencies:**
- None (pure TypeScript)

**Key Features:**
- Configurable capacity (default 7)
- Time-based decay (TTL)
- Priority-based retention
- LRU eviction policy
- Rehearsal mechanism
- Automatic cleanup

**Test Cases:**
- Add 10 items to capacity-7 cache, verify eviction
- Test item decay after TTL expires
- Verify rehearsal extends item lifetime
- Test priority-based retention
- Measure access patterns

---

## Agent 4: Episodic Memory Agent 📚

### Brain Analogy: Hippocampus

**Biological Basis:**
- **Location:** Medial temporal lobe
- **Function:** Encoding and consolidation of episodic memories
- **Mechanism:**
  - Pattern separation (distinguish similar experiences)
  - Pattern completion (recall full memory from partial cue)
  - Temporal sequence encoding (order of events)
  - Spatial context binding (where did it happen)
  - Sleep consolidation (replay during slow-wave sleep)
- **Properties:**
  - Fast encoding (single exposure)
  - Context-dependent retrieval
  - Gradual transfer to cortex over time
  - Critical for "what-where-when" binding

**Cognitive Process:**
The hippocampus stores your life experiences. When you remember your first day of school, a birthday party, or what you had for breakfast, you're accessing episodic memory. The hippocampus binds together: **what** happened (content), **where** it happened (spatial context), **when** it happened (temporal context), and **how** you felt (emotional context).

**Famous Case:** Patient H.M. had his hippocampus removed and could no longer form new episodic memories, though he retained old memories and could learn skills.

**Memory Consolidation:**
- **Encoding:** Create memory trace (~seconds)
- **Consolidation:** Transfer to long-term storage (hours to years)
- **Retrieval:** Reactivate memory trace (~200-500ms)

**Neurotransmitters:**
- Glutamate (encoding)
- GABA (pattern separation)
- Acetylcholine (consolidation)

**Computational Essence:**
Associative storage with rich contextual indexing and semantic similarity search.

### TypeScript Implementation

**Complexity:** ⭐⭐⭐

**Core Functionality:**
- Store experiences with rich metadata
- Semantic search via embeddings
- Context-based retrieval
- Pattern completion

**Interface:**
```typescript
interface EpisodicMemory {
  id: string;
  content: string;
  embedding?: number[]; // semantic vector
  context: {
    timestamp: Date;
    location?: string;
    participants?: string[];
    activity?: string;
    emotionalValence?: number; // -1 to 1
    emotionalArousal?: number; // 0 to 1
    tags?: string[];
  };
  consolidationScore: number; // 0-1, increases over time
  retrievalCount: number;
  relatedMemories?: string[]; // IDs of associated memories
}

interface MemoryQuery {
  content?: string;
  contextFilters?: {
    dateRange?: { start: Date; end: Date };
    location?: string;
    participants?: string[];
    tags?: string[];
    emotionalRange?: { min: number; max: number };
  };
  similarityThreshold?: number;
  limit?: number;
}

interface MemorySearchResult {
  memory: EpisodicMemory;
  relevanceScore: number;
  matchedFactors: string[];
}

class EpisodicMemoryAgent {
  private memories: Map<string, EpisodicMemory>;
  private embeddingService: EmbeddingService; // OpenAI, Cohere, etc.

  constructor(embeddingService: EmbeddingService) {
    this.embeddingService = embeddingService;
    this.memories = new Map();
  }

  // Store a new episodic memory
  async store(
    content: string,
    context: EpisodicMemory['context']
  ): Promise<string>;

  // Retrieve memories by semantic similarity
  async recall(query: MemoryQuery): Promise<MemorySearchResult[]>;

  // Pattern completion: partial cue → full memory
  async complete(partialCue: string): Promise<EpisodicMemory | null>;

  // Consolidate memory (strengthen over time)
  consolidate(memoryId: string): void;

  // Link related memories
  associateMemories(memoryId1: string, memoryId2: string): void;

  // Get memories from time period
  getTemporalContext(startDate: Date, endDate: Date): EpisodicMemory[];

  // Forget (decay) old, unretrieved memories
  decay(threshold: number): number;

  // Get memory statistics
  getStats(): {
    totalMemories: number;
    averageConsolidation: number;
    mostRetrievedMemory: EpisodicMemory;
  };
}
```

**Dependencies:**
- Embedding service (OpenAI SDK, Cohere, or local model)
- Vector similarity library (e.g., `vectra`, `hnswlib-node`)

**Key Features:**
- Semantic search using embeddings
- Rich contextual metadata
- Pattern completion
- Memory consolidation over time
- Associative linking
- Temporal and spatial context

**Test Cases:**
- Store 100 memories with varied contexts
- Retrieve by semantic similarity
- Filter by time, location, emotion
- Test pattern completion with partial cues
- Verify consolidation strengthens memories

---

## Agent 5: Reward Learning Agent 🎁

### Brain Analogy: Basal Ganglia + Dopaminergic System

**Biological Basis:**
- **Location:**
  - Striatum (caudate, putamen)
  - Substantia nigra (dopamine source)
  - Ventral tegmental area (VTA - reward signaling)
- **Function:** Action selection through reward learning
- **Mechanism:**
  - Dopamine signals prediction error (surprise)
  - Positive error: reward better than expected → strengthen action
  - Negative error: reward worse than expected → weaken action
  - Builds action-outcome associations
- **Properties:**
  - Trial-and-error learning
  - Gradual habit formation through repetition
  - "Direct pathway" (Go) vs "Indirect pathway" (NoGo)
  - Critical for motivation and addiction

**Cognitive Process:**
The basal ganglia learns "If I do X in situation Y, I get reward Z." Through dopamine-mediated reinforcement, successful actions are strengthened and unsuccessful ones weakened. This is how you learn to ride a bike, play a game, or navigate a new city - through trial, error, and reward feedback.

**Temporal Difference Learning:**
- Brain uses TD algorithm (discovered in neuroscience, then AI)
- Dopamine firing = prediction error
- Unexpected reward: dopamine burst
- Expected reward: no change
- Reward omitted: dopamine dip

**Neurotransmitters:**
- **Dopamine:** Reward prediction error signal
- **Acetylcholine:** Modulates learning rate
- **GABA:** Inhibits competing actions

**Habit Formation:**
- Early: goal-directed (prefrontal cortex involved)
- Late: habitual (basal ganglia autonomous)
- Transition happens with repetition (~weeks)

**Computational Essence:**
Q-learning / Temporal Difference learning - updating action values based on reward feedback.

### TypeScript Implementation

**Complexity:** ⭐⭐⭐

**Core Functionality:**
- Learn action values through rewards
- Q-learning or TD-learning
- Epsilon-greedy exploration
- Habit formation tracking

**Interface:**
```typescript
interface State {
  id: string;
  features: Record<string, any>;
}

interface Action {
  id: string;
  name: string;
  parameters?: Record<string, any>;
}

interface Experience {
  state: State;
  action: Action;
  reward: number;
  nextState: State;
  timestamp: Date;
}

interface LearningParams {
  learningRate: number; // alpha (0-1)
  discountFactor: number; // gamma (0-1)
  explorationRate: number; // epsilon (0-1)
  explorationDecay: number; // reduce exploration over time
}

interface ActionValue {
  action: Action;
  qValue: number;
  timesSelected: number;
  averageReward: number;
}

class RewardLearningAgent {
  private qTable: Map<string, Map<string, number>>; // state -> action -> Q-value
  private params: LearningParams;
  private experienceHistory: Experience[];

  constructor(params?: Partial<LearningParams>) {
    this.params = {
      learningRate: 0.1,
      discountFactor: 0.9,
      explorationRate: 0.2,
      explorationDecay: 0.995,
      ...params
    };
    this.qTable = new Map();
    this.experienceHistory = [];
  }

  // Select action for given state (epsilon-greedy)
  selectAction(state: State, possibleActions: Action[]): Action;

  // Update Q-values based on experience
  learn(experience: Experience): number; // returns TD error (dopamine signal)

  // Get Q-value for state-action pair
  getQValue(state: State, action: Action): number;

  // Get best action for state (exploitation)
  getBestAction(state: State, possibleActions: Action[]): Action;

  // Get action statistics
  getActionStats(state: State): ActionValue[];

  // Detect habit formation (high Q-value, many repetitions)
  isHabitFormed(state: State, action: Action): boolean;

  // Decay exploration rate over time
  decayExploration(): void;

  // Get learning statistics
  getStats(): {
    totalExperiences: number;
    averageReward: number;
    explorationRate: number;
    habitsFormed: number;
  };
}
```

**Dependencies:**
- None (pure TypeScript)

**Key Features:**
- Q-learning implementation
- Epsilon-greedy exploration
- TD error calculation (dopamine analogue)
- Habit detection
- Experience replay
- Exploration decay

**Test Cases:**
- Learn optimal path in grid world
- Test exploration vs exploitation balance
- Verify Q-values converge to optimal
- Detect habit formation after repetitions
- Test credit assignment over time

---

## Agent 6: Emotional Tagging Agent 💗

### Brain Analogy: Amygdala + Limbic System

**Biological Basis:**
- **Location:**
  - Amygdala (medial temporal lobe)
  - Insula (interoceptive awareness)
  - Anterior cingulate (emotional regulation)
- **Function:**
  - Detect emotional significance of stimuli
  - Fast threat detection (~20ms via thalamus shortcut)
  - Tag memories with emotional valence
  - Modulate attention and memory encoding
- **Mechanism:**
  - Parallel processing of emotional features
  - Amygdala lesions → inability to recognize fear
  - Fear conditioning (Pavlovian learning)
  - Modulates hippocampus (emotional memories stronger)
- **Properties:**
  - Fast, unconscious processing
  - Valence dimension: positive ↔ negative
  - Arousal dimension: calm ↔ excited
  - Survival-critical (predators, food, mates)

**Cognitive Process:**
The amygdala acts as your emotional alarm system. It rapidly evaluates stimuli for emotional significance before you're consciously aware. A spider, a smiling face, or a loud noise triggers the amygdala, which then amplifies or dampens other brain processes. Emotional arousal enhances memory encoding - you remember emotional events more vividly.

**Two-Route Processing:**
- **Fast route:** Thalamus → Amygdala (~20ms, crude "is it dangerous?")
- **Slow route:** Thalamus → Cortex → Amygdala (~200ms, detailed "what exactly is it?")

**Emotional Dimensions:**
- **Valence:** Positive (pleasure) ↔ Negative (pain)
- **Arousal:** High (excited) ↔ Low (calm)
- **Dominance:** In control ↔ Controlled

**Fear Conditioning:**
- Neutral stimulus + aversive outcome = learned fear
- Very rapid learning (one trial)
- Resistant to extinction
- Basis of phobias and PTSD

**Neurotransmitters:**
- **Norepinephrine:** Arousal, stress
- **Serotonin:** Mood regulation
- **GABA:** Inhibits amygdala (anxiolytics work here)

**Computational Essence:**
Rapid valence and arousal scoring to modulate other processes (attention, memory, decision-making).

### TypeScript Implementation

**Complexity:** ⭐⭐⭐

**Core Functionality:**
- Score emotional valence and arousal
- Tag content with emotions
- Modulate memory encoding
- Fast threat detection

**Interface:**
```typescript
interface EmotionalResponse {
  valence: number; // -1 (negative) to +1 (positive)
  arousal: number; // 0 (calm) to 1 (excited)
  dominance?: number; // 0 (controlled) to 1 (in control)
  discreteEmotion?: 'joy' | 'fear' | 'anger' | 'sadness' | 'disgust' | 'surprise';
  confidence: number; // 0-1
  processingTime: number; // ms
}

interface EmotionalContext {
  recentEmotions: EmotionalResponse[];
  baselineMood: number; // -1 to 1
  stressLevel: number; // 0 to 1
  emotionalMemories: Array<{ stimulus: string; emotion: EmotionalResponse }>;
}

interface EmotionalModulation {
  attentionBoost: number; // multiplier for attention
  memoryStrength: number; // multiplier for encoding
  urgency: number; // action priority modifier
  approach: boolean; // approach vs avoid
}

class EmotionalTaggingAgent {
  private context: EmotionalContext;
  private sentimentAnalyzer: SentimentAnalyzer; // NLP model
  private conditionedAssociations: Map<string, EmotionalResponse>;

  constructor(sentimentAnalyzer: SentimentAnalyzer) {
    this.sentimentAnalyzer = sentimentAnalyzer;
    this.context = {
      recentEmotions: [],
      baselineMood: 0,
      stressLevel: 0,
      emotionalMemories: []
    };
    this.conditionedAssociations = new Map();
  }

  // Evaluate emotional content of stimulus
  async evaluate(stimulus: string): Promise<EmotionalResponse>;

  // Fast threat detection (bypass detailed analysis)
  detectThreat(stimulus: string): { isThreat: boolean; confidence: number };

  // Classical conditioning: associate stimulus with emotion
  condition(stimulus: string, emotion: EmotionalResponse): void;

  // Get conditioned emotional response
  getConditionedResponse(stimulus: string): EmotionalResponse | null;

  // Calculate how emotion modulates other processes
  getModulation(emotion: EmotionalResponse): EmotionalModulation;

  // Tag memory with emotional significance
  tagMemory(content: string, emotion: EmotionalResponse): {
    content: string;
    emotion: EmotionalResponse;
    encodingStrength: number;
  };

  // Update emotional context (mood, stress)
  updateContext(updates: Partial<EmotionalContext>): void;

  // Get current emotional state
  getCurrentState(): EmotionalContext;

  // Regulate emotion (prefrontal cortex influence)
  regulate(targetValence: number, strategy: 'reappraisal' | 'suppression'): void;
}
```

**Dependencies:**
- Sentiment analysis library (e.g., `sentiment`, `compromise`, or API like OpenAI)
- Optional: emotion detection model

**Key Features:**
- Valence-arousal-dominance scoring
- Fast threat detection pathway
- Classical conditioning
- Memory encoding modulation
- Emotional context tracking
- Emotion regulation

**Test Cases:**
- Score emotional valence of sentences
- Detect threats in stimuli
- Test conditioning (neutral + negative → fear)
- Verify high arousal boosts memory strength
- Test emotion regulation strategies

---

## Agent 7: Goal Stack Agent 🎯

### Brain Analogy: Prefrontal Cortex (Goal Hierarchy)

**Biological Basis:**
- **Location:**
  - Dorsolateral PFC (goal maintenance)
  - Anterior PFC (goal hierarchy, branching)
  - Orbitofrontal cortex (goal value)
- **Function:** Hierarchical goal management and planning
- **Mechanism:**
  - Maintain multiple goals simultaneously
  - Hierarchical decomposition (goals → subgoals)
  - Context-dependent goal activation
  - Goal switching and inhibition
- **Properties:**
  - Hierarchical structure (big goal → small steps)
  - Goal persistence despite distractions
  - Proactive vs reactive goal pursuit
  - Resource competition between goals

**Cognitive Process:**
The prefrontal cortex manages your goal hierarchy. When you decide "I want to make dinner," the PFC breaks this into subgoals: check ingredients, decide recipe, cook, serve. Each subgoal may have further sub-subgoals. The PFC maintains this stack, tracks progress, and switches between goals as needed.

**Goal Hierarchies:**
- **Abstract goals:** "Be successful" (years)
- **Concrete goals:** "Get promoted" (months)
- **Proximal goals:** "Finish project" (weeks)
- **Immediate actions:** "Write report" (hours)

**Goal Characteristics:**
- **Specificity:** Vague vs concrete
- **Temporality:** Short-term vs long-term
- **Priority:** Critical vs optional
- **Dependencies:** Sequential vs parallel

**Neural Dynamics:**
- **Goal activation:** Sustained PFC firing
- **Goal completion:** Reward signal (dopamine)
- **Goal switching:** ACC conflict detection
- **Goal failure:** Negative prediction error

**Computational Essence:**
A hierarchical stack data structure with priority management and decomposition logic.

### TypeScript Implementation

**Complexity:** ⭐⭐⭐

**Core Functionality:**
- Hierarchical goal management
- Goal decomposition
- Priority tracking
- Progress monitoring

**Interface:**
```typescript
interface Goal {
  id: string;
  description: string;
  status: 'pending' | 'active' | 'completed' | 'failed' | 'suspended';
  priority: number; // 0-10
  deadline?: Date;
  parentGoalId?: string;
  subGoals: string[]; // IDs of child goals
  requiredActions: Action[];
  completedActions: Action[];
  estimatedTime?: number; // minutes
  actualTime?: number;
  createdAt: Date;
  startedAt?: Date;
  completedAt?: Date;
  metadata?: {
    category?: string;
    tags?: string[];
    context?: string;
  };
}

interface GoalProgress {
  goal: Goal;
  percentComplete: number;
  completedSubGoals: number;
  totalSubGoals: number;
  completedActions: number;
  totalActions: number;
  isOnTrack: boolean;
  estimatedCompletion?: Date;
}

interface GoalConflict {
  goal1: Goal;
  goal2: Goal;
  conflictType: 'time' | 'resource' | 'dependency';
  severity: number;
}

class GoalStackAgent {
  private goals: Map<string, Goal>;
  private activeGoalStack: string[]; // Stack of active goal IDs

  constructor() {
    this.goals = new Map();
    this.activeGoalStack = [];
  }

  // Add a new goal
  addGoal(
    description: string,
    priority: number,
    parentGoalId?: string,
    deadline?: Date
  ): string;

  // Decompose goal into subgoals
  decomposeGoal(goalId: string, subGoals: string[]): void;

  // Push goal onto active stack
  activateGoal(goalId: string): void;

  // Get current active goal (top of stack)
  getCurrentGoal(): Goal | null;

  // Complete current goal and pop from stack
  completeGoal(goalId: string): void;

  // Switch to different goal
  switchGoal(newGoalId: string): void;

  // Suspend goal (remove from stack but keep)
  suspendGoal(goalId: string): void;

  // Get goal progress
  getProgress(goalId: string): GoalProgress;

  // Get all goals at a hierarchy level
  getGoalsAtLevel(level: number): Goal[];

  // Detect goal conflicts
  detectConflicts(): GoalConflict[];

  // Get goals by priority
  getGoalsByPriority(minPriority: number): Goal[];

  // Prune completed/failed goals
  pruneGoals(): number;
}
```

**Dependencies:**
- None (pure TypeScript)

**Key Features:**
- Hierarchical goal structure
- Goal stack (LIFO)
- Progress tracking
- Deadline monitoring
- Conflict detection
- Priority management

**Test Cases:**
- Create goal hierarchy (3 levels deep)
- Test goal activation/deactivation
- Track progress on composite goals
- Detect conflicting deadlines
- Test goal switching

---

## Agent 8: Simple Planning Agent 📋

### Brain Analogy: Dorsolateral Prefrontal Cortex (Planning) + Parietal Cortex (Mental Simulation)

**Biological Basis:**
- **Location:**
  - Dorsolateral PFC (plan generation)
  - Parietal cortex (spatial reasoning, mental simulation)
  - Premotor cortex (action sequencing)
- **Function:** Generate action sequences to achieve goals
- **Mechanism:**
  - Mental simulation of future states
  - Forward planning (imagine outcomes)
  - Backward chaining (work backwards from goal)
  - Evaluation of alternative plans
- **Properties:**
  - ~3-5 steps ahead for most people
  - Mental models of environment
  - Counterfactual reasoning ("what if")
  - Plan flexibility and replanning

**Cognitive Process:**
When you plan how to get somewhere, solve a puzzle, or organize a project, your prefrontal cortex generates a sequence of actions. It mentally simulates "if I do X, then Y will happen, then I can do Z." Planning involves creating a mental model of the world and testing action sequences in your imagination.

**Planning Strategies:**
- **Forward planning:** Start from current state, work towards goal
- **Backward planning:** Start from goal, work backwards to current state
- **Hill climbing:** Take actions that get closer to goal
- **Means-ends analysis:** Reduce difference between current and goal state

**Famous Tasks:**
- **Tower of Hanoi:** Move disks between pegs following rules
- **Wisconsin Card Sort:** Discover rule through trial and error
- **Traveling salesman:** Find optimal route

**Neural Activity:**
- PFC shows sustained activity during planning phase
- Parietal cortex active during mental rotation/simulation
- Hippocampus reactivates during planning (memory of similar situations)

**Computational Essence:**
STRIPS-like planning: state space search with preconditions and effects.

### TypeScript Implementation

**Complexity:** ⭐⭐⭐⭐

**Core Functionality:**
- Generate action sequences
- State space search
- Plan evaluation
- Replanning when needed

**Interface:**
```typescript
interface State {
  id: string;
  facts: Set<string>; // propositions true in this state
  timestamp?: Date;
}

interface Action {
  id: string;
  name: string;
  preconditions: Set<string>; // must be true to execute
  effects: {
    add: Set<string>; // facts added by action
    remove: Set<string>; // facts removed by action
  };
  cost: number; // resource cost or time
}

interface Plan {
  id: string;
  goal: Goal;
  actions: Action[];
  estimatedCost: number;
  confidence: number; // 0-1
  createdAt: Date;
  status: 'proposed' | 'executing' | 'completed' | 'failed';
  currentStep: number;
}

interface PlanningProblem {
  initialState: State;
  goalState: State;
  availableActions: Action[];
  constraints?: {
    maxSteps?: number;
    maxCost?: number;
    requiredActions?: string[];
    forbiddenActions?: string[];
  };
}

class SimplePlanningAgent {
  private plans: Map<string, Plan>;
  private executionHistory: Array<{ plan: Plan; outcome: 'success' | 'failure' }>;

  constructor() {
    this.plans = new Map();
    this.executionHistory = [];
  }

  // Generate plan using forward search
  generatePlan(problem: PlanningProblem): Plan | null;

  // Check if action is applicable in state
  isApplicable(action: Action, state: State): boolean;

  // Apply action to state (compute next state)
  applyAction(action: Action, state: State): State;

  // Check if goal is satisfied
  isGoalSatisfied(state: State, goal: State): boolean;

  // Evaluate plan quality
  evaluatePlan(plan: Plan): { cost: number; feasibility: number; quality: number };

  // Find alternative plans
  generateAlternatives(problem: PlanningProblem, count: number): Plan[];

  // Replan when execution fails
  replan(failedPlan: Plan, currentState: State): Plan | null;

  // Execute plan step by step
  async executePlan(
    planId: string,
    executeAction: (action: Action) => Promise<boolean>
  ): Promise<boolean>;

  // Get plan execution status
  getPlanStatus(planId: string): {
    plan: Plan;
    progress: number;
    stepsCompleted: number;
    stepsRemaining: number;
  };
}
```

**Dependencies:**
- None (pure TypeScript, but could use A* or planning library)

**Key Features:**
- Forward state-space search
- Precondition checking
- Effect application
- Plan evaluation
- Replanning capability
- Multiple plan generation

**Test Cases:**
- Solve Tower of Hanoi (3 disks)
- Plan route in grid with obstacles
- Generate multi-step recipe plan
- Test replanning when action fails
- Compare alternative plans

---

## Agent 9: Divergent Idea Generator 💡

### Brain Analogy: Default Mode Network (DMN)

**Biological Basis:**
- **Location:**
  - Medial prefrontal cortex
  - Posterior cingulate cortex
  - Precuneus
  - Medial temporal lobe
- **Function:** Spontaneous thought, creativity, mind-wandering
- **Mechanism:**
  - Active during rest (anti-correlated with task-focused networks)
  - Spontaneous memory retrieval and recombination
  - Mental time travel (past and future simulation)
  - Self-referential thinking
- **Properties:**
  - "Task-negative" network
  - Involved in creativity, insight, problem-solving
  - Connects disparate memories and concepts
  - Active during "aha!" moments

**Cognitive Process:**
The DMN is active when you're not focused on external tasks - daydreaming, showering, walking. This is when creative insights often occur. The DMN retrieves random memories and concepts, recombines them in novel ways, and generates spontaneous ideas. This is the neural basis of divergent thinking - generating many varied ideas.

**DMN vs ECN:**
- **DMN (Default Mode):** Divergent, associative, creative, spontaneous
- **ECN (Executive Control):** Convergent, focused, evaluative, deliberate
- **Creativity:** Alternation between DMN (generate) and ECN (evaluate)

**Creative Process:**
1. **Preparation:** Learn about problem (ECN)
2. **Incubation:** Let DMN wander, make connections
3. **Illumination:** Insight! ("Aha!")
4. **Verification:** Evaluate and refine (ECN)

**Divergent Thinking Tests:**
- **Alternative Uses Test:** List unusual uses for a brick
- **Consequences Test:** What if humans didn't need sleep?
- **Remote Associates Test:** Find word connecting "cottage, swiss, cake" (cheese)

**Computational Essence:**
Stochastic exploration of semantic/conceptual space with low constraint.

### TypeScript Implementation

**Complexity:** ⭐⭐⭐⭐

**Core Functionality:**
- Generate diverse ideas
- Semantic exploration
- Random association
- Novelty scoring

**Interface:**
```typescript
interface Idea {
  id: string;
  content: string;
  novelty: number; // 0-1 (how different from existing ideas)
  feasibility?: number; // 0-1 (how realistic)
  sourceMemories?: string[]; // IDs of memories that inspired it
  associations: string[]; // related concepts
  generatedAt: Date;
}

interface DivergentPrompt {
  seed: string; // starting concept
  domain?: string; // constrain to domain
  constraints?: {
    mustInclude?: string[];
    mustAvoid?: string[];
    minNovelty?: number;
  };
  quantity: number; // how many ideas to generate
  diversity: number; // 0-1, how different they should be
}

interface ConceptSpace {
  concepts: Map<string, string[]>; // concept -> related concepts
  semanticDistance: (a: string, b: string) => number;
}

class DivergentIdeaGenerator {
  private conceptSpace: ConceptSpace;
  private generatedIdeas: Idea[];
  private llmService?: LLMService; // optional for enhanced generation

  constructor(conceptSpace: ConceptSpace, llmService?: LLMService) {
    this.conceptSpace = conceptSpace;
    this.llmService = llmService;
    this.generatedIdeas = [];
  }

  // Generate ideas through free association
  async generateIdeas(prompt: DivergentPrompt): Promise<Idea[]>;

  // Random walk through concept space
  randomWalk(startConcept: string, steps: number): string[];

  // Combine concepts in novel ways
  combineconcepts(concepts: string[]): string;

  // Calculate novelty relative to existing ideas
  calculateNovelty(idea: string, existingIdeas: Idea[]): number;

  // Filter for diversity (remove similar ideas)
  diversify(ideas: Idea[], targetCount: number): Idea[];

  // Generate by analogy (A:B :: C:?)
  generateByAnalogy(a: string, b: string, c: string): string[];

  // Remote associates (find connecting concept)
  findRemoteAssociate(words: string[]): string | null;

  // Score idea fluency, flexibility, originality
  scoreCreativity(ideas: Idea[]): {
    fluency: number; // quantity
    flexibility: number; // variety of categories
    originality: number; // average novelty
  };

  // Get inspiration from episodic memories
  async getInspiration(memoryAgent: EpisodicMemoryAgent): Promise<string[]>;
}
```

**Dependencies:**
- Optional: LLM API (OpenAI, Anthropic) for enhanced generation
- Embedding service for semantic distance
- Concept graph/knowledge base

**Key Features:**
- Stochastic idea generation
- Semantic random walk
- Concept combination
- Novelty scoring
- Diversity enforcement
- Analogical reasoning
- Remote associates

**Test Cases:**
- Generate 20 ideas from prompt
- Test novelty calculation
- Verify diversity enforcement
- Test analogical reasoning
- Measure fluency/flexibility/originality
- Compare with/without LLM

---

## Agent 10: Performance Monitor Agent 📊

### Brain Analogy: Medial Prefrontal Cortex (mPFC) - Metacognition

**Biological Basis:**
- **Location:**
  - Medial prefrontal cortex (Brodmann area 10)
  - Anterior prefrontal cortex
  - Frontopolar cortex
- **Function:** Self-monitoring, metacognition, introspection
- **Mechanism:**
  - Monitor own cognitive processes
  - Estimate confidence in decisions
  - Detect errors and uncertainty
  - Evaluate strategy effectiveness
- **Properties:**
  - "Thinking about thinking"
  - Critical for self-awareness
  - Develops late (adolescence)
  - Correlates with intelligence

**Cognitive Process:**
Metacognition is your ability to monitor and evaluate your own thinking. When you think "I'm not sure about this answer" or "I need to change my approach," that's metacognition. The mPFC tracks performance, estimates confidence, and triggers strategy changes when needed.

**Metacognitive Functions:**
- **Monitoring:** Track progress and performance
- **Control:** Adjust strategies based on monitoring
- **Confidence:** Judge certainty of beliefs/decisions
- **Source monitoring:** Did I see it or imagine it?

**Metacognitive Judgments:**
- **Feeling of knowing:** "I know this, it's on the tip of my tongue"
- **Judgment of learning:** "I've mastered this material"
- **Confidence:** "I'm 80% sure this is correct"
- **Ease of learning:** "This will be hard to learn"

**Error Detection:**
- **Error-related negativity (ERN):** Brain signal ~50-100ms after error
- **Medial PFC:** Detects conflict and errors
- **Triggers:** Corrective action or strategy change

**Neural Correlates:**
- mPFC damage → impaired self-monitoring
- mPFC activity correlates with confidence ratings
- mPFC links to theory of mind (understanding others' minds)

**Computational Essence:**
Self-referential monitoring loop that tracks system performance and triggers adaptation.

### TypeScript Implementation

**Complexity:** ⭐⭐⭐⭐

**Core Functionality:**
- Track performance metrics
- Confidence estimation
- Strategy evaluation
- Trigger adaptations

**Interface:**
```typescript
interface PerformanceMetric {
  timestamp: Date;
  taskId: string;
  taskType: string;
  outcome: 'success' | 'failure' | 'partial';
  confidence: number; // 0-1, agent's confidence
  actualCorrectness?: boolean; // ground truth
  responseTime: number; // ms
  strategy: string;
  metadata?: Record<string, any>;
}

interface StrategyPerformance {
  strategyName: string;
  successRate: number;
  averageConfidence: number;
  calibration: number; // confidence vs actual accuracy
  averageResponseTime: number;
  usageCount: number;
  lastUsed: Date;
}

interface PerformanceSummary {
  overallAccuracy: number;
  averageConfidence: number;
  calibration: number; // |confidence - accuracy|
  totalTasks: number;
  recentTrend: 'improving' | 'stable' | 'declining';
  weakAreas: string[];
  strongAreas: string[];
  recommendedActions: string[];
}

interface Adaptation {
  trigger: string; // what caused adaptation
  oldStrategy: string;
  newStrategy: string;
  timestamp: Date;
  rationale: string;
}

class PerformanceMonitorAgent {
  private metrics: PerformanceMetric[];
  private strategies: Map<string, StrategyPerformance>;
  private adaptations: Adaptation[];
  private confidenceThreshold: number;
  private windowSize: number; // how many recent tasks to analyze

  constructor(confidenceThreshold: number = 0.6, windowSize: number = 50) {
    this.metrics = [];
    this.strategies = new Map();
    this.adaptations = [];
    this.confidenceThreshold = confidenceThreshold;
    this.windowSize = windowSize;
  }

  // Log a task performance
  logPerformance(metric: PerformanceMetric): void;

  // Estimate confidence for current task
  estimateConfidence(
    taskType: string,
    currentState: any
  ): { confidence: number; basis: string };

  // Check if performance is declining
  detectDecline(windowSize?: number): boolean;

  // Evaluate strategy effectiveness
  evaluateStrategy(strategyName: string): StrategyPerformance;

  // Recommend strategy change
  recommendStrategy(taskType: string): string | null;

  // Calculate calibration (confidence vs accuracy alignment)
  calculateCalibration(windowSize?: number): number;

  // Get performance summary
  getSummary(): PerformanceSummary;

  // Should agent ask for help?
  shouldRequestHelp(): boolean;

  // Trigger adaptation based on performance
  adapt(): Adaptation | null;

  // Compare strategies
  compareStrategies(strategy1: string, strategy2: string): {
    better: string;
    reason: string;
    difference: number;
  };

  // Get recent performance trend
  getTrend(windowSize?: number): {
    direction: 'improving' | 'stable' | 'declining';
    magnitude: number;
  };
}
```

**Dependencies:**
- None (pure TypeScript)
- Optional: Statistical analysis library for trends

**Key Features:**
- Performance logging and tracking
- Confidence estimation
- Calibration (confidence vs accuracy)
- Strategy evaluation
- Decline detection
- Automatic adaptation
- Help-seeking triggers

**Test Cases:**
- Track 100 task performances
- Calculate calibration score
- Detect performance decline
- Test strategy recommendation
- Trigger adaptation on decline
- Verify help-seeking behavior

---

## Implementation Order Summary

### Phase 1: Core Infrastructure (Weeks 1-2)
1. **Pattern Recognition Agent** - Simplest, no dependencies
2. **Attention Filter Agent** - Simple filtering logic
3. **Working Memory Agent** - Basic cache with eviction

### Phase 2: Memory & Learning (Weeks 3-4)
4. **Episodic Memory Agent** - Requires embedding service
5. **Reward Learning Agent** - Q-learning implementation

### Phase 3: Emotion & Goals (Weeks 5-6)
6. **Emotional Tagging Agent** - Sentiment analysis
7. **Goal Stack Agent** - Hierarchical goals

### Phase 4: Planning & Creativity (Weeks 7-8)
8. **Simple Planning Agent** - STRIPS-like planning
9. **Divergent Idea Generator** - Creative exploration

### Phase 5: Metacognition (Week 9)
10. **Performance Monitor Agent** - Self-monitoring

---

## Technology Stack

### Required
- **Runtime:** Node.js 18+
- **Language:** TypeScript 5+
- **Testing:** Jest or Vitest
- **Linting:** ESLint + Prettier

### Optional (by agent)
- **Embedding:** OpenAI SDK, Cohere, or local models
- **Sentiment:** `sentiment` npm package or API
- **LLM:** OpenAI, Anthropic (for idea generation)
- **Vector DB:** `vectra`, `hnswlib-node` (for memory)

### Development Tools
- **Package manager:** npm or pnpm
- **Build:** tsup or tsc
- **Docs:** TypeDoc
- **Monitoring:** Winston (logging)

---

## Next Steps

1. **Set up project structure:**
```bash
mkdir csal-agents
cd csal-agents
npm init -y
npm install -D typescript @types/node jest @types/jest
npx tsc --init
```

2. **Create agent template:**
```typescript
// src/agents/BaseAgent.ts
export abstract class BaseAgent {
  abstract name: string;
  abstract brainAnalogue: string;

  abstract process(input: any): Promise<any>;

  getInfo() {
    return {
      name: this.name,
      brainAnalogue: this.brainAnalogue
    };
  }
}
```

3. **Implement Agent 1** (Pattern Recognition)

4. **Write tests:**
```typescript
// src/agents/__tests__/PatternRecognitionAgent.test.ts
import { PatternRecognitionAgent } from '../PatternRecognitionAgent';

describe('PatternRecognitionAgent', () => {
  it('should detect email patterns', () => {
    const agent = new PatternRecognitionAgent();
    // ... tests
  });
});
```

5. **Document each agent** as you build

---

**Ready to start building cognitive AI agents!** 🚀🧠
