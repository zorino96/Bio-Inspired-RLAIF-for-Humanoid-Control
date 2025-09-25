# Algorithm: Reinforcement Learning from AI Feedback (RLAIF) for Humanoid Learning

This document details the step-by-step conceptual algorithm for the "15 Minutes of Evolution" experiment, which serves as a proof-of-concept for our proposed framework.

**Initialization:**

1.  Initialize the **Humanoid Environment** (`Env`) in a physics simulator like PyBullet.
2.  Initialize the **Cellular Brain** (`Brain`) with random parameters `θ`.
    *   The `Brain` is a `CellAssembly` network, a large, distributed collection of simple cells.
3.  Initialize the **VLM Teacher** (`Teacher`) by loading a pre-trained Vision-Language Model (e.g., LLaVA-1.5 7B).
4.  Initialize an **Optimizer** (e.g., Adam) for the `Brain`'s parameters `θ`.
5.  Initialize an empty list for storing the `best_behavior_frames` and set a `highest_score` tracker to a very low value.
6.  Set a `start_time` for the training loop.

---

**Main Training Loop:**

**WHILE** `current_time - start_time` is less than the total training duration (e.g., 900 seconds):

1.  **Reset & Observe:**
    *   Reset the `Env` to its initial, stable state.
    *   Get the initial observation `S_before` from the environment's sensors.
    *   Render the initial image `I_before = Env.render()`.

2.  **Generate Action:**
    *   Convert the observation `S_before` into a tensor `T_S_before`.
    *   Generate an action tensor `T_A = Brain(T_S_before)`. The brain's cells collectively produce this action.

3.  **Execute & Record:**
    *   Convert the action tensor `T_A` to a NumPy array `A` compatible with the environment.
    *   Initialize an empty list `current_frames` and add the initial image `I_before` to it.
    *   **FOR** a fixed number of simulation steps (e.g., `t = 1 to 120`) **DO**:
        *   Execute the action `A` in the `Env`.
        *   Periodically render the current state (`I_t`) and add it to `current_frames`.
    *   Render the final image of the sequence, `I_after = Env.render()`.

4.  **Get Teacher's Feedback:**
    *   Combine `I_before` and `I_after` into a single panoramic image, `I_comparison`.
    *   Provide `I_comparison` and a high-level prompt (e.g., "did the robot become more stable?") to the `Teacher`.
    *   Receive the scalar reward `R = Teacher.evaluate(I_comparison)`.

5.  **Learn (Update the Brain):**
    *   Calculate the policy loss based on the action and the received reward: `Loss = -mean(T_A) * R`.
    *   Perform backpropagation to update the brain's parameters `θ`:
        *   `Optimizer.zero_grad()`
        *   `Loss.backward()`
        *   `Optimizer.step()`

6.  **Store Best Behavior:**
    *   **IF** the reward `R` is greater than `highest_score` **THEN**:
        *   Update `highest_score = R`.
        *   Store the `current_frames` as the new `best_behavior_frames`.

**END WHILE**

---

**Final Output:**

1.  After the loop finishes, save the `best_behavior_frames` as a video file.
2.  The final output is a demonstration of the most successful behavior learned by the agent during the training session.
