---
layout: projects
title: Inferno
external: https://buas.itch.io/inferno
image: /assets/images/enemies_showcase.gif
description: University project where 2 programmers, 5 designers, and 11 artists were tasked with expanding a third-person speedrunning prototype to a full-fledged game in 8 weeks. I was a technical lead on the team.
tags:
  - Student Project
  - Unreal Engine
  - Jenkins
  - AI & Gameplay
  - PC
---

<p>
  <ul>
    <li>Second big university project where we made a game in 8 weeks. The design team made a prototype for the game beforehand, and together, we fleshed out their concept to a full-fledged game. Improving design concepts, technical implementation, and the art. I acted as a technical lead, but, with only 2 programmers, there was not much to lead. Therefore, I mostly acted as a gateway for communication between the leads and the rest of the team. Technical issues that popped up would be directed to me, and I would make a plan of attack to resolve it most of the time. Whenever designers came up with a new feature, they came to me to discuss the technical possibilities of it.
    </li>
    <li>
      <h2>📝 Responsibilities</h2>
      <p>Acting as technical lead with only 2 programmers in the team removes part of the responsibility of a technical lead, but that was compensated since I worked on more programming tasks. I still tried to help my team in whatever way possible. I did not have to manage programmers, dividing tasks, and ensuring code quality. I did, however, try to be involved with the other programmer's work, asking for updates, also how the team communication was going, and just in general being a point of contact for the other programmer to come to with concerns.
      <br>
      On the other side I tried to be actively involved with the design lead, visual artist lead, and producer regarding the status of the project. What is the progress of the programmers, planning concerns, team communication, and preparing progress presentations for our stakeholders. More on the technical side, but still important work as a technical lead, I was responsible for maintaining builds of our game. Uploading the newest version on Itch.io, creating new test builds for the team to conduct playtests, and setting up an automatic build pipeline using Jenkins.
      </p>
    </li>
    <li>
      <h2>👾 Enemy AI</h2>
      <p>Enemies in Inferno are static monsters that interact with the player in some way. One enemy shoots a projectile at the player, another explodes and launches the player upwards, one enemy requires the player to shoot its shields first before being able to defeat it, and the final enemy acts as a launchpad where it launches the player in one of four cardinal directions.
      <br>
      <img src="/assets/images/Inferno/enemies_blueprint_ac_shoot.png" style="width:100%; height:auto;">
      <br>
      <img src="/assets/images/Inferno/enemies_blueprint_ac_shoot_logic.png" style="width:100%; height:auto;">
      <br>
      The most important challenge enemies can provide is by reducing the player's health through projectiles. The tricky part is to find a balance between challenge, and punishment. During playtesting players reported that enemies felt too punishing because they were still able to shoot the player even if the player was already 'past' that enemy. As a solution to this problem, designers asked if we could introduce a radius in which enemies attack the player, but don't do anything if they're outside. It was a basic change, with the implementation shown in the images above, but it improved the player-experience significantly.
      <br>
      One bug we encountered late into the development cycle happened because enemies always tried to rotate towards the player, no matter the distance. Since enemies don't damage the player when making direct contact, it resulted in the following unfortunate, although funny, situation:
      <br>
      <video width="400px" height="auto" autoplay muted loop controls controlsList="nodownload nofullscreen noremoteplayback">
        <source src="/assets/images/Inferno/bug_rotating_enemy.mp4" type="video/mp4">
      </video>
      <br>
      The solution I came up with was to have a minimum distance between the player and enemy before the enemy starts rotating. Another issue I addressed was the fact the enemy was rotating on the pitch axis as well, which results in the enemy looking like its sunbathing while trying to attack the player. The new and improved implementation is as follows:
      <br>
      <img src="/assets/images/Inferno/enemies_blueprint_calculate_rotation.png" style="width:100%; height:auto;">
      <br>
      While it might look slightly messy, the logic is relatively simple. We retrieve the player's location and check whether it is below the distance threshold between the enemy and the player. If it is, we retrieve the enemy's rotation and the rotation the enemy would need to look at the player. Finally we interpolate between those values to smoothly rotate the enemy towards the player on the yaw axis.
      </p>
    </li>
    <li>
      <h2>🌐 Offline & Online Leaderboard</h2>
      <p>Encouraging players to keep improving their time was a major driving factor to implement an offline, as well as an online leaderboard to submit your fastest times. The offline leaderboard would track all the times set on the local machine, while the online leaderboard would include the singular fastest time of any player. 
      <br>
      Due to time constraint (and knowledge) we did not have time to create a custom backend for storing and tracking run times. Instead we decided to use Supabase as our online leaderboard. We could communicate with Supabase through HTTP Requests, which we implemented in Blueprints using Epic's experimental plugin for HTTP Requests. To limit the possibilities of interacting with the leaderboard in unexpected ways, we left as much logic that changed values in the leaderboard to Supabase, and not in Blueprints. For example, players can submit their time to the online leaderboard, but they don't directly interact with the database, Supabase has functionality to handle user-sent data so that part is abstracted from the Blueprints logic. For example, the following function in Supabase receives a time from a player and updates the corresponding entry in the table if the time is faster than the existing time.
      <br>
      <img src="/assets/images/Inferno/supabase_edge_function.png" style="width:100%; height:auto;">
      <br>
      We still wanted some way to control what names and, specifically, what characters are allowed. Unreal Engine has no predefined regex functionality, so I opted to write my own. 
      <br>
      <img src="/assets/images/Inferno/blueprint_regex_1.png" style="width:100%; height:auto;">
      <br>
      It starts by removing trailing whitespaces at the start and end.
      <br>
      <img src="/assets/images/Inferno/blueprint_regex_2.png" style="width:100%; height:auto;">
      <br>
      Next, the length of the name is tested against a length determined by the designers for minimum name length. If the provided name does not meet the requirements, the user is informed why the name was wrong, and they can enter a new name.
      <br>
      <img src="/assets/images/Inferno/blueprint_regex_3.png" style="width:100%; height:auto;">
      <br>
      Slightly more tedious to set up but very valuable for control was checking for forbidden characters. There is no functionality for determining if there is a special character included in a string. We want to prevent users from using special characters that might escape its intended scope, but also want control over what characters that include. The solution was to create an array of forbidden characters. It was more of a setup to manually fill in all the forbidden characters, but now, if we want to include or exclude a certain character, the setup does not need to change at all. The character is simply added or removed from the array. The provided name is tested against the forbidden characters, and if a forbidden character is encountered, the user is informed and can enter a new name. The full implementation of this basic regex is shown in the following video.
      <br>
      <video width="500px" height="auto" autoplay muted loop controls controlsList="nodownload nofullscreen noremoteplayback">
        <source src="/assets/images/Inferno/leaderboard_regex_and_availability.mp4" type="video/mp4">
      </video>
      <br>
      </p>
    </li>
    <li>  
      <iframe width="420" height="315"
      src="https://www.youtube.com/embed/gPxhpy_uWUY?autoplay=1&mute=1">
      </iframe> 
    </li>
  </ul>
</p>
