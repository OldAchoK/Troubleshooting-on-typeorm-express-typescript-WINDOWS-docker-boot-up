<h2>Troubleshooting-on-typeorm-express-typescript-WINDOWS-docker-boot-up</h2>
<h3> With help of teachers Igor Perekrestov and Serhyi Sherba
<br> And fellow student Anton Hurzidze</h3>
<br>
<h2> Defining the problem</h2>
<p> After cloning git repo to WebStorm IDE and building containers<br>
 on windows you could encounter such errors:</p>
<p>
  -  unable to get image...<br>
  -  ERROR: connect ECONNREFUSED<br>
  -  ERROR: unable to select packages:<br>
 (no such package):  |   bash<br>
  -  ERROR: NODE_PATH is not defined(smth like that)<br>
</p>
<h2> Unable to get image </h2>
<p> SOLUTION: Boot up Docker Desktop, if you don't have such, then download it.</p>
<br>
<h2> ERROR: NODE_PATH is not defined(smth like that) </h2>
<p> If such problem appears than Solution will be:</p>
<p>
  -  open packages.json
  -  change parameter on line 8 <br>
  RESULT: "start": "NODE_PATH=./src node app.js",<br>
  -  change three lines on numbers 6, 21, 26 adding to the second json argument "cross-env"<br>
  RESULT: "dev": "cross-env debug=* NODE_PATH=./src ts-node-dev --respawn ./src/index.ts",<br>
          "migration:run": "cross-env NODE_PATH=./src ts-node ./node_modules/typeorm/cli.js migration:run --config ./src/orm/config/ormconfig.ts",<br>
          "seed:run": "cross-env NODE_PATH=./src ts-node ./node_modules/.bin/typeorm migration:run --config ./src/orm/config/ormconfig-seed.ts",<br>
  This commands will help commands not conflicting with Windows syntax or whatever.
</p>
<br>
<h2> ERROR: unable to select packages: (no such package):  |   bash<br> </h2>
<p> Such error signals that bash scripts don't work properly in your environment, so the solution:</p>
<p>
  -  if your containers are working open them in Docker Desktop<br>
  -  open your containers group(it simply copy name of ur WebStorm project)<br>
  -  open be_boilerplate container<br>
  -  open EXEC tab<br>
  -  when terminal starts paste such command "which bash"<br>
  -  if there is nothing then skip one next step<br>
  -  if there is the path to bash derictory than copy it<br>
  -  find "scripts" folder in your derictory and open both of them<br>
  -  on first line of each script u could see directory of the executable Shell<br>
  -  change it to look: #!(your strict copied path) or if there is nothing copied: #!/bin/bash<br>
</p>
<br>
<h2> ERROR: connect ECONNREFUSED</h2>
<p> At first I would advice to check all previous solutions because this one could simply be mask of other root problems<br>
 If there is nothing helped then check ur docker-compose.dev.yml container image and .env file<br>
 They must have on lines 11 (container image file) and 7 (.env) have ports and there must be followed such rule:<br>
 '????(your numbers):5432' and PG_PORT=5432, the numbers that are defined must be like that no other way</p>
 <br>
 <h2> Some alien symbols on failed DataBase connection</h2>
 <img src="/img/6.png">
 <p> Most of us have other disciplines and on some we could simply make busy such port as 5432<br>
  So to avoid problem of connection open docker-compose.dev.yml container image file<br>
  and change line 11 to such look '????(your numbers):5432'<br>
  and change port to your numbers on DataBase connection properties</p>
 <br>
 <h2>"cross-env" error</h2>
 <img src="/img/5.png">
 <p> If after debugging program you face such error than simply "rollback" your package.json</p>
 <br>
 <h2> In conclusion</h2>
 <p> In this topic was described most common problems that have me and my fellow students on setting up this proj on WINDOWS<br>
  If there is something else that wasn't mentioned in this guide remember - I miss the part where this is my problem</p>
