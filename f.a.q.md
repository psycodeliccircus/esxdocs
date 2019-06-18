---
description: Esta página tem algumas dicas úteis para todo o ES Extended.
---

# F.A.Q

## Ordem de Início FiveM

{% hint style="warning" %}
Quando você está baixando scripts, especialmente os scripts **ES Extended**, existem "**requisitos**".   
Quais são vitais para eles funcionando corretamente.   
A ordem de início dos seus scripts no seu **`server.cfg`** é importante.   
Os requisitos para um script devem estar acima do script que o exige, se for carregado posteriormente, o script pode não funcionar como pretendido.   
Portanto, ter sua ordem de partida correta é vital.
{% endhint %}

```text
endpoint_add_tcp "0.0.0.0:30120"
endpoint_add_udp "0.0.0.0:30120"

set mysql_connection_string "server=adress;database=dbname;userid=user;password=psswd"
set es_enableCustomData 1
set sv_licenseKey "XXXXXXXXXXXXXXXXXXX"
sv_scriptHookAllowed 0
rcon_password blablablabla
sv_hostname "ESX BRASIL PUBLIC SERVER"
set temp_convar "ESX"

# desativar o anúncio? limpar o mestre, descomentando este
#sv_master1 ""

# deseja permitir apenas jogadores autenticados com um provedor de terceiros como o Steam?
sv_authMaxVariance 1
sv_authMinTrust 1

# adicionar administradores do sistema
add_ace group.admin command allow # allow all commands
add_ace group.admin command.quit deny # but don't allow quit
add_ace resource.essentialmode command.add_ace allow
add_ace resource.essentialmode command.add_principal allow
add_principal identifier.steam:XXXXXXXXXXXXX group.admin # add the admin to the group

# ocultar pontos de extremidade do player na saída de log externo
sv_endpointprivacy true

#### FIVEM DEFAULT ####
start mapmanager
start chat
start spawnmanager
start sessionmanager
restart sessionmanager
start fivem
start hardcap
start rconlog
start scoreboard
start baseevents

#### MYSQL ASYNC
start mysql-async

#### ESSENTIAL MODS
start essentialmode
start esplugin_mysql
start es_admin2
start es_extended
start es_camera

#### ESX NECESSÁRIO MODS
start instance
start cron
start esx_identity
start skinchanger
start esx_skin
start esx_menu_default
start esx_menu_list
start esx_menu_dialog
start esx_phone
start esx_addonaccount
start esx_addoninventory
start esx_datastore
start esx_society
start esx_service
start esx_billing
start esx_animations
start esx_license
start esx_optionalneeds
start esx_sit

#### ESX TRABALHOS
start esx_jobs
start esx_joblisting
start esx_taxijob
start esx_mechanicjob
start esx_policejob
start esx_property
start esx_realestateagentjob
start esx_bankerjob
start esx_ambulancejob
start esx_vehicleshop
start esx_tattooshop
start esx_barbershop
start esx_boilerplate
start esx_shops
start esx_accessories
start esx_weaponshop

#### ESX QUALQUER OUTROS MODS
start esx_status
start esx_basicneeds
start esx_clotheshop
start esx_garage
start esx_holdup
start esx_drugs
start esx_atm
start esx_cruisecontrol
start esx_voice
start esx_whitelistEnhanced
start esx_lscustom
start esx_boat
start esx_rpchat

#### QUALQUER MODO NÃO ESX
#start nonESXmod
```

## **EXEMPLO BANCO DE DADOS**

```text
/*
 Navicat Premium Data Transfer

 Source Server         : server local
 Source Server Type    : MySQL
 Source Server Version : 100138
 Source Host           : localhost:3306
 Source Schema         : essentialmode

 Target Server Type    : MySQL
 Target Server Version : 100138
 File Encoding         : 65001

 Date: 16/05/2019 05:15:03
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for addon_account
-- ----------------------------
DROP TABLE IF EXISTS `addon_account`;
CREATE TABLE `addon_account`  (
  `name` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `label` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `shared` int(11) NOT NULL,
  PRIMARY KEY (`name`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of addon_account
-- ----------------------------
INSERT INTO `addon_account` VALUES ('bank_savings', 'Livreto azul', 0);
INSERT INTO `addon_account` VALUES ('caution', 'Cuidado', 0);
INSERT INTO `addon_account` VALUES ('property_black_money', 'Propriedade de venda de dinheiro', 0);
INSERT INTO `addon_account` VALUES ('society_ambulance', 'Ambulância', 1);
INSERT INTO `addon_account` VALUES ('society_banker', 'Banco', 1);
INSERT INTO `addon_account` VALUES ('society_cardealer', 'Concessionária', 1);
INSERT INTO `addon_account` VALUES ('society_mechanic', 'Mecânico', 1);
INSERT INTO `addon_account` VALUES ('society_police', 'Polícia', 1);
INSERT INTO `addon_account` VALUES ('society_realestateagent', 'Agente imobiliário', 1);
INSERT INTO `addon_account` VALUES ('society_taxi', 'Taxi', 1);

-- ----------------------------
-- Table structure for addon_account_data
-- ----------------------------
DROP TABLE IF EXISTS `addon_account_data`;
CREATE TABLE `addon_account_data`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `account_name` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `money` double NOT NULL,
  `owner` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for addon_inventory
-- ----------------------------
DROP TABLE IF EXISTS `addon_inventory`;
CREATE TABLE `addon_inventory`  (
  `name` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `label` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `shared` int(11) NOT NULL,
  PRIMARY KEY (`name`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of addon_inventory
-- ----------------------------
INSERT INTO `addon_inventory` VALUES ('property', 'Propriedade', 0);
INSERT INTO `addon_inventory` VALUES ('society_ambulance', 'Ambulância', 1);
INSERT INTO `addon_inventory` VALUES ('society_cardealer', 'Concessionária', 1);
INSERT INTO `addon_inventory` VALUES ('society_mechanic', 'Mecânico', 1);
INSERT INTO `addon_inventory` VALUES ('society_police', 'Polícia', 1);
INSERT INTO `addon_inventory` VALUES ('society_taxi', 'Taxi', 1);

-- ----------------------------
-- Table structure for addon_inventory_items
-- ----------------------------
DROP TABLE IF EXISTS `addon_inventory_items`;
CREATE TABLE `addon_inventory_items`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `inventory_name` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `name` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `count` int(11) NOT NULL,
  `owner` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for billing
-- ----------------------------
DROP TABLE IF EXISTS `billing`;
CREATE TABLE `billing`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `identifier` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `sender` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `target_type` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `target` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `label` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `amount` int(11) NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for cardealer_vehicles
-- ----------------------------
DROP TABLE IF EXISTS `cardealer_vehicles`;
CREATE TABLE `cardealer_vehicles`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `vehicle` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `price` int(11) NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for characters
-- ----------------------------
DROP TABLE IF EXISTS `characters`;
CREATE TABLE `characters`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `identifier` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `firstname` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `lastname` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `dateofbirth` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `sex` varchar(1) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL DEFAULT 'M',
  `height` varchar(128) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for datastore
-- ----------------------------
DROP TABLE IF EXISTS `datastore`;
CREATE TABLE `datastore`  (
  `name` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `label` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `shared` int(11) NOT NULL,
  PRIMARY KEY (`name`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of datastore
-- ----------------------------
INSERT INTO `datastore` VALUES ('property', 'Propriedade', 0);
INSERT INTO `datastore` VALUES ('society_ambulance', 'Ambulância', 1);
INSERT INTO `datastore` VALUES ('society_police', 'Polícia', 1);
INSERT INTO `datastore` VALUES ('society_taxi', 'Taxi', 1);
INSERT INTO `datastore` VALUES ('user_ears', 'Orelhas', 0);
INSERT INTO `datastore` VALUES ('user_glasses', 'Oculos', 0);
INSERT INTO `datastore` VALUES ('user_helmet', 'Capacete', 0);
INSERT INTO `datastore` VALUES ('user_mask', 'Mascarar', 0);

-- ----------------------------
-- Table structure for datastore_data
-- ----------------------------
DROP TABLE IF EXISTS `datastore_data`;
CREATE TABLE `datastore_data`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `owner` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `data` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL,
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE INDEX `unique_datastore_owner_name`(`owner`, `name`) USING BTREE,
  INDEX `index_datastore_name`(`name`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for fine_types
-- ----------------------------
DROP TABLE IF EXISTS `fine_types`;
CREATE TABLE `fine_types`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `label` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `amount` int(11) NULL DEFAULT NULL,
  `category` int(11) NULL DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 53 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of fine_types
-- ----------------------------
INSERT INTO `fine_types` VALUES (1, 'Abuso de autoridade', 30, 0);
INSERT INTO `fine_types` VALUES (2, 'Cruzar uma linha contínua', 40, 0);
INSERT INTO `fine_types` VALUES (3, 'Tráfego contracorrente', 250, 0);
INSERT INTO `fine_types` VALUES (4, 'Reviravolta não autorizada', 250, 0);
INSERT INTO `fine_types` VALUES (5, 'Tráfego off-road', 170, 0);
INSERT INTO `fine_types` VALUES (6, 'Não respeitar as distâncias de segurança', 30, 0);
INSERT INTO `fine_types` VALUES (7, 'Parada Perigosa / Proibida', 150, 0);
INSERT INTO `fine_types` VALUES (8, 'Estacionamento inábil / proibido', 70, 0);
INSERT INTO `fine_types` VALUES (9, 'Não respeitando a prioridade à direita', 70, 0);
INSERT INTO `fine_types` VALUES (10, 'Não cumprimento de um veículo prioritário', 90, 0);
INSERT INTO `fine_types` VALUES (11, 'O não cumprimento de uma parada', 105, 0);
INSERT INTO `fine_types` VALUES (12, 'Incumprimento de um sinal vermelho', 130, 0);
INSERT INTO `fine_types` VALUES (13, 'Ultrapassagem perigosa', 100, 0);
INSERT INTO `fine_types` VALUES (14, 'Veículo não em estado', 100, 0);
INSERT INTO `fine_types` VALUES (15, 'Condução sem licença', 1500, 0);
INSERT INTO `fine_types` VALUES (16, 'Bata e corra', 800, 0);
INSERT INTO `fine_types` VALUES (17, 'Excesso de velocidade <5 km / h', 90, 0);
INSERT INTO `fine_types` VALUES (18, 'Excesso de velocidade 5-15 km h', 120, 0);
INSERT INTO `fine_types` VALUES (19, 'Excesso de velocidade  15-30 kmh', 180, 0);
INSERT INTO `fine_types` VALUES (20, 'Excesso de velocidade > 30 kmh', 300, 0);
INSERT INTO `fine_types` VALUES (21, 'Obstrução do tráfego', 110, 1);
INSERT INTO `fine_types` VALUES (22, 'Degradação da via pública', 90, 1);
INSERT INTO `fine_types` VALUES (23, 'Bloqueio de via pública', 90, 1);
INSERT INTO `fine_types` VALUES (24, 'Obstruindo operação policial', 130, 1);
INSERT INTO `fine_types` VALUES (25, 'Insulto entre civis', 75, 1);
INSERT INTO `fine_types` VALUES (26, 'Indignação ao policial', 110, 1);
INSERT INTO `fine_types` VALUES (27, 'Ameaça ou intimidação verbal em relação a civil', 90, 1);
INSERT INTO `fine_types` VALUES (28, 'Ameaça verbal ou intimidação de um policial', 150, 1);
INSERT INTO `fine_types` VALUES (29, 'Protesto ilegal', 250, 1);
INSERT INTO `fine_types` VALUES (30, 'Tentativa de corrupção', 1500, 1);
INSERT INTO `fine_types` VALUES (31, 'Arma branca na cidade', 120, 2);
INSERT INTO `fine_types` VALUES (32, 'Arma letal na cidade', 300, 2);
INSERT INTO `fine_types` VALUES (33, 'Porta de Arma Não Permitida (Falha de Licença)', 600, 2);
INSERT INTO `fine_types` VALUES (34, 'Porto de arma ilegal', 700, 2);
INSERT INTO `fine_types` VALUES (35, 'Reconhecido lockpick bandeira', 300, 2);
INSERT INTO `fine_types` VALUES (36, 'Roubo de carro', 1800, 2);
INSERT INTO `fine_types` VALUES (37, 'Venda de drogas', 1500, 2);
INSERT INTO `fine_types` VALUES (38, 'Fabricação de medicamentos', 1500, 2);
INSERT INTO `fine_types` VALUES (39, 'Posse de drogas', 650, 2);
INSERT INTO `fine_types` VALUES (40, 'civil tomada de reféns', 1500, 2);
INSERT INTO `fine_types` VALUES (41, 'Agente de aquisição do estado', 2000, 2);
INSERT INTO `fine_types` VALUES (42, 'Roubar casas', 650, 2);
INSERT INTO `fine_types` VALUES (43, 'Roubar loja', 650, 2);
INSERT INTO `fine_types` VALUES (44, 'Assalto a banco', 1500, 2);
INSERT INTO `fine_types` VALUES (45, 'Atira em um civil', 2000, 3);
INSERT INTO `fine_types` VALUES (46, 'Atira em um agente do estado', 2500, 3);
INSERT INTO `fine_types` VALUES (47, 'Tentativa de homicídio em civil', 3000, 3);
INSERT INTO `fine_types` VALUES (48, 'Tentativa de assassinato em um agente do estado', 5000, 3);
INSERT INTO `fine_types` VALUES (49, 'Assassinato de um civil', 10000, 3);
INSERT INTO `fine_types` VALUES (50, 'Assassinato de um agente do estadual', 30000, 3);
INSERT INTO `fine_types` VALUES (51, 'Assassinato involuntariamente', 1800, 3);
INSERT INTO `fine_types` VALUES (52, 'Golpe de negócios', 2000, 2);

-- ----------------------------
-- Table structure for items
-- ----------------------------
DROP TABLE IF EXISTS `items`;
CREATE TABLE `items`  (
  `name` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `label` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `limit` int(11) NOT NULL DEFAULT -1,
  `rare` int(11) NOT NULL DEFAULT 0,
  `can_remove` int(11) NOT NULL DEFAULT 1,
  PRIMARY KEY (`name`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of items
-- ----------------------------
INSERT INTO `items` VALUES ('alive_chicken', 'Frango vivo', 20, 0, 1);
INSERT INTO `items` VALUES ('bandage', 'Bandagem', 20, 0, 1);
INSERT INTO `items` VALUES ('blowpipe', 'Maçaricos', 10, 0, 1);
INSERT INTO `items` VALUES ('bread', 'Pão', 10, 0, 1);
INSERT INTO `items` VALUES ('cannabis', 'Folha de Maconha', 40, 0, 1);
INSERT INTO `items` VALUES ('carokit', 'Kit body', 3, 0, 1);
INSERT INTO `items` VALUES ('carotool', 'Ferramentas body', 4, 0, 1);
INSERT INTO `items` VALUES ('clothe', 'Vestuário', 40, 0, 1);
INSERT INTO `items` VALUES ('copper', 'Cobre', 56, 0, 1);
INSERT INTO `items` VALUES ('cutted_wood', 'Madeira cortada', 20, 0, 1);
INSERT INTO `items` VALUES ('diamond', 'Diamante', 50, 0, 1);
INSERT INTO `items` VALUES ('essence', 'Essence', 24, 0, 1);
INSERT INTO `items` VALUES ('fabric', 'Pano', 80, 0, 1);
INSERT INTO `items` VALUES ('fish', 'Peixe', 100, 0, 1);
INSERT INTO `items` VALUES ('fixkit', 'Kit de reparação', 5, 0, 1);
INSERT INTO `items` VALUES ('fixtool', 'Ferramentas de reparo', 6, 0, 1);
INSERT INTO `items` VALUES ('gazbottle', 'Garrafa de gás', 11, 0, 1);
INSERT INTO `items` VALUES ('gold', 'Ouro', 21, 0, 1);
INSERT INTO `items` VALUES ('iron', 'Ferro', 42, 0, 1);
INSERT INTO `items` VALUES ('marijuana', 'Maconha', 14, 0, 1);
INSERT INTO `items` VALUES ('medikit', 'Kit médico', 5, 0, 1);
INSERT INTO `items` VALUES ('packaged_chicken', 'Frango em uma bandeja', 100, 0, 1);
INSERT INTO `items` VALUES ('packaged_plank', 'Embalagem de pranchas', 100, 0, 1);
INSERT INTO `items` VALUES ('petrol', 'Óleo', 24, 0, 1);
INSERT INTO `items` VALUES ('petrol_raffin', 'Óleo Refinado', 24, 0, 1);
INSERT INTO `items` VALUES ('slaughtered_chicken', 'Frango abatido', 20, 0, 1);
INSERT INTO `items` VALUES ('stone', 'Pedra', 7, 0, 1);
INSERT INTO `items` VALUES ('washed_stone', 'Pedra lavada', 7, 0, 1);
INSERT INTO `items` VALUES ('water', 'água', 5, 0, 1);
INSERT INTO `items` VALUES ('wood', 'Madeira', 20, 0, 1);
INSERT INTO `items` VALUES ('wool', 'Lã', 40, 0, 1);

-- ----------------------------
-- Table structure for job_grades
-- ----------------------------
DROP TABLE IF EXISTS `job_grades`;
CREATE TABLE `job_grades`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `job_name` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `grade` int(11) NOT NULL,
  `name` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `label` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `salary` int(11) NOT NULL,
  `skin_male` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `skin_female` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 41 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of job_grades
-- ----------------------------
INSERT INTO `job_grades` VALUES (1, 'unemployed', 0, 'unemployed', 'Desempregado', 200, '{}', '{}');
INSERT INTO `job_grades` VALUES (2, 'lumberjack', 0, 'employee', 'Empregado', 0, '{}', '{}');
INSERT INTO `job_grades` VALUES (3, 'fisherman', 0, 'employee', 'Empregado', 0, '{}', '{}');
INSERT INTO `job_grades` VALUES (4, 'fueler', 0, 'employee', 'Empregado', 0, '{}', '{}');
INSERT INTO `job_grades` VALUES (5, 'reporter', 0, 'employee', 'Empregado', 0, '{}', '{}');
INSERT INTO `job_grades` VALUES (6, 'tailor', 0, 'employee', 'Empregado', 0, '{\"mask_1\":0,\"arms\":1,\"glasses_1\":0,\"hair_color_2\":4,\"makeup_1\":0,\"face\":19,\"glasses\":0,\"mask_2\":0,\"makeup_3\":0,\"skin\":29,\"helmet_2\":0,\"lipstick_4\":0,\"sex\":0,\"torso_1\":24,\"makeup_2\":0,\"bags_2\":0,\"chain_2\":0,\"ears_1\":-1,\"bags_1\":0,\"bproof_1\":0,\"shoes_2\":0,\"lipstick_2\":0,\"chain_1\":0,\"tshirt_1\":0,\"eyebrows_3\":0,\"pants_2\":0,\"beard_4\":0,\"torso_2\":0,\"beard_2\":6,\"ears_2\":0,\"hair_2\":0,\"shoes_1\":36,\"tshirt_2\":0,\"beard_3\":0,\"hair_1\":2,\"hair_color_1\":0,\"pants_1\":48,\"helmet_1\":-1,\"bproof_2\":0,\"eyebrows_4\":0,\"eyebrows_2\":0,\"decals_1\":0,\"age_2\":0,\"beard_1\":5,\"shoes\":10,\"lipstick_1\":0,\"eyebrows_1\":0,\"glasses_2\":0,\"makeup_4\":0,\"decals_2\":0,\"lipstick_3\":0,\"age_1\":0}', '{\"mask_1\":0,\"arms\":5,\"glasses_1\":5,\"hair_color_2\":4,\"makeup_1\":0,\"face\":19,\"glasses\":0,\"mask_2\":0,\"makeup_3\":0,\"skin\":29,\"helmet_2\":0,\"lipstick_4\":0,\"sex\":1,\"torso_1\":52,\"makeup_2\":0,\"bags_2\":0,\"chain_2\":0,\"ears_1\":-1,\"bags_1\":0,\"bproof_1\":0,\"shoes_2\":1,\"lipstick_2\":0,\"chain_1\":0,\"tshirt_1\":23,\"eyebrows_3\":0,\"pants_2\":0,\"beard_4\":0,\"torso_2\":0,\"beard_2\":6,\"ears_2\":0,\"hair_2\":0,\"shoes_1\":42,\"tshirt_2\":4,\"beard_3\":0,\"hair_1\":2,\"hair_color_1\":0,\"pants_1\":36,\"helmet_1\":-1,\"bproof_2\":0,\"eyebrows_4\":0,\"eyebrows_2\":0,\"decals_1\":0,\"age_2\":0,\"beard_1\":5,\"shoes\":10,\"lipstick_1\":0,\"eyebrows_1\":0,\"glasses_2\":0,\"makeup_4\":0,\"decals_2\":0,\"lipstick_3\":0,\"age_1\":0}');
INSERT INTO `job_grades` VALUES (7, 'miner', 0, 'employee', 'Empregado', 0, '{\"tshirt_2\":1,\"ears_1\":8,\"glasses_1\":15,\"torso_2\":0,\"ears_2\":2,\"glasses_2\":3,\"shoes_2\":1,\"pants_1\":75,\"shoes_1\":51,\"bags_1\":0,\"helmet_2\":0,\"pants_2\":7,\"torso_1\":71,\"tshirt_1\":59,\"arms\":2,\"bags_2\":0,\"helmet_1\":0}', '{}');
INSERT INTO `job_grades` VALUES (8, 'slaughterer', 0, 'employee', 'Empregado', 0, '{\"age_1\":0,\"glasses_2\":0,\"beard_1\":5,\"decals_2\":0,\"beard_4\":0,\"shoes_2\":0,\"tshirt_2\":0,\"lipstick_2\":0,\"hair_2\":0,\"arms\":67,\"pants_1\":36,\"skin\":29,\"eyebrows_2\":0,\"shoes\":10,\"helmet_1\":-1,\"lipstick_1\":0,\"helmet_2\":0,\"hair_color_1\":0,\"glasses\":0,\"makeup_4\":0,\"makeup_1\":0,\"hair_1\":2,\"bproof_1\":0,\"bags_1\":0,\"mask_1\":0,\"lipstick_3\":0,\"chain_1\":0,\"eyebrows_4\":0,\"sex\":0,\"torso_1\":56,\"beard_2\":6,\"shoes_1\":12,\"decals_1\":0,\"face\":19,\"lipstick_4\":0,\"tshirt_1\":15,\"mask_2\":0,\"age_2\":0,\"eyebrows_3\":0,\"chain_2\":0,\"glasses_1\":0,\"ears_1\":-1,\"bags_2\":0,\"ears_2\":0,\"torso_2\":0,\"bproof_2\":0,\"makeup_2\":0,\"eyebrows_1\":0,\"makeup_3\":0,\"pants_2\":0,\"beard_3\":0,\"hair_color_2\":4}', '{\"age_1\":0,\"glasses_2\":0,\"beard_1\":5,\"decals_2\":0,\"beard_4\":0,\"shoes_2\":0,\"tshirt_2\":0,\"lipstick_2\":0,\"hair_2\":0,\"arms\":72,\"pants_1\":45,\"skin\":29,\"eyebrows_2\":0,\"shoes\":10,\"helmet_1\":-1,\"lipstick_1\":0,\"helmet_2\":0,\"hair_color_1\":0,\"glasses\":0,\"makeup_4\":0,\"makeup_1\":0,\"hair_1\":2,\"bproof_1\":0,\"bags_1\":0,\"mask_1\":0,\"lipstick_3\":0,\"chain_1\":0,\"eyebrows_4\":0,\"sex\":1,\"torso_1\":49,\"beard_2\":6,\"shoes_1\":24,\"decals_1\":0,\"face\":19,\"lipstick_4\":0,\"tshirt_1\":9,\"mask_2\":0,\"age_2\":0,\"eyebrows_3\":0,\"chain_2\":0,\"glasses_1\":5,\"ears_1\":-1,\"bags_2\":0,\"ears_2\":0,\"torso_2\":0,\"bproof_2\":0,\"makeup_2\":0,\"eyebrows_1\":0,\"makeup_3\":0,\"pants_2\":0,\"beard_3\":0,\"hair_color_2\":4}');
INSERT INTO `job_grades` VALUES (9, 'cardealer', 0, 'recruit', 'Recruta', 10, '{}', '{}');
INSERT INTO `job_grades` VALUES (10, 'cardealer', 1, 'novice', 'Novato', 25, '{}', '{}');
INSERT INTO `job_grades` VALUES (11, 'cardealer', 2, 'experienced', 'Experimente', 40, '{}', '{}');
INSERT INTO `job_grades` VALUES (12, 'cardealer', 3, 'boss', 'Patrão', 0, '{}', '{}');
INSERT INTO `job_grades` VALUES (13, 'taxi', 0, 'recrue', 'Recruta', 12, '{\"hair_2\":0,\"hair_color_2\":0,\"torso_1\":32,\"bags_1\":0,\"helmet_2\":0,\"chain_2\":0,\"eyebrows_3\":0,\"makeup_3\":0,\"makeup_2\":0,\"tshirt_1\":31,\"makeup_1\":0,\"bags_2\":0,\"makeup_4\":0,\"eyebrows_4\":0,\"chain_1\":0,\"lipstick_4\":0,\"bproof_2\":0,\"hair_color_1\":0,\"decals_2\":0,\"pants_2\":0,\"age_2\":0,\"glasses_2\":0,\"ears_2\":0,\"arms\":27,\"lipstick_1\":0,\"ears_1\":-1,\"mask_2\":0,\"sex\":0,\"lipstick_3\":0,\"helmet_1\":-1,\"shoes_2\":0,\"beard_2\":0,\"beard_1\":0,\"lipstick_2\":0,\"beard_4\":0,\"glasses_1\":0,\"bproof_1\":0,\"mask_1\":0,\"decals_1\":1,\"hair_1\":0,\"eyebrows_2\":0,\"beard_3\":0,\"age_1\":0,\"tshirt_2\":0,\"skin\":0,\"torso_2\":0,\"eyebrows_1\":0,\"face\":0,\"shoes_1\":10,\"pants_1\":24}', '{\"hair_2\":0,\"hair_color_2\":0,\"torso_1\":57,\"bags_1\":0,\"helmet_2\":0,\"chain_2\":0,\"eyebrows_3\":0,\"makeup_3\":0,\"makeup_2\":0,\"tshirt_1\":38,\"makeup_1\":0,\"bags_2\":0,\"makeup_4\":0,\"eyebrows_4\":0,\"chain_1\":0,\"lipstick_4\":0,\"bproof_2\":0,\"hair_color_1\":0,\"decals_2\":0,\"pants_2\":1,\"age_2\":0,\"glasses_2\":0,\"ears_2\":0,\"arms\":21,\"lipstick_1\":0,\"ears_1\":-1,\"mask_2\":0,\"sex\":1,\"lipstick_3\":0,\"helmet_1\":-1,\"shoes_2\":0,\"beard_2\":0,\"beard_1\":0,\"lipstick_2\":0,\"beard_4\":0,\"glasses_1\":5,\"bproof_1\":0,\"mask_1\":0,\"decals_1\":1,\"hair_1\":0,\"eyebrows_2\":0,\"beard_3\":0,\"age_1\":0,\"tshirt_2\":0,\"skin\":0,\"torso_2\":0,\"eyebrows_1\":0,\"face\":0,\"shoes_1\":49,\"pants_1\":11}');
INSERT INTO `job_grades` VALUES (14, 'taxi', 1, 'novice', 'Novato', 24, '{\"hair_2\":0,\"hair_color_2\":0,\"torso_1\":32,\"bags_1\":0,\"helmet_2\":0,\"chain_2\":0,\"eyebrows_3\":0,\"makeup_3\":0,\"makeup_2\":0,\"tshirt_1\":31,\"makeup_1\":0,\"bags_2\":0,\"makeup_4\":0,\"eyebrows_4\":0,\"chain_1\":0,\"lipstick_4\":0,\"bproof_2\":0,\"hair_color_1\":0,\"decals_2\":0,\"pants_2\":0,\"age_2\":0,\"glasses_2\":0,\"ears_2\":0,\"arms\":27,\"lipstick_1\":0,\"ears_1\":-1,\"mask_2\":0,\"sex\":0,\"lipstick_3\":0,\"helmet_1\":-1,\"shoes_2\":0,\"beard_2\":0,\"beard_1\":0,\"lipstick_2\":0,\"beard_4\":0,\"glasses_1\":0,\"bproof_1\":0,\"mask_1\":0,\"decals_1\":1,\"hair_1\":0,\"eyebrows_2\":0,\"beard_3\":0,\"age_1\":0,\"tshirt_2\":0,\"skin\":0,\"torso_2\":0,\"eyebrows_1\":0,\"face\":0,\"shoes_1\":10,\"pants_1\":24}', '{\"hair_2\":0,\"hair_color_2\":0,\"torso_1\":57,\"bags_1\":0,\"helmet_2\":0,\"chain_2\":0,\"eyebrows_3\":0,\"makeup_3\":0,\"makeup_2\":0,\"tshirt_1\":38,\"makeup_1\":0,\"bags_2\":0,\"makeup_4\":0,\"eyebrows_4\":0,\"chain_1\":0,\"lipstick_4\":0,\"bproof_2\":0,\"hair_color_1\":0,\"decals_2\":0,\"pants_2\":1,\"age_2\":0,\"glasses_2\":0,\"ears_2\":0,\"arms\":21,\"lipstick_1\":0,\"ears_1\":-1,\"mask_2\":0,\"sex\":1,\"lipstick_3\":0,\"helmet_1\":-1,\"shoes_2\":0,\"beard_2\":0,\"beard_1\":0,\"lipstick_2\":0,\"beard_4\":0,\"glasses_1\":5,\"bproof_1\":0,\"mask_1\":0,\"decals_1\":1,\"hair_1\":0,\"eyebrows_2\":0,\"beard_3\":0,\"age_1\":0,\"tshirt_2\":0,\"skin\":0,\"torso_2\":0,\"eyebrows_1\":0,\"face\":0,\"shoes_1\":49,\"pants_1\":11}');
INSERT INTO `job_grades` VALUES (15, 'taxi', 2, 'experimente', 'Experimente', 36, '{\"hair_2\":0,\"hair_color_2\":0,\"torso_1\":26,\"bags_1\":0,\"helmet_2\":0,\"chain_2\":0,\"eyebrows_3\":0,\"makeup_3\":0,\"makeup_2\":0,\"tshirt_1\":57,\"makeup_1\":0,\"bags_2\":0,\"makeup_4\":0,\"eyebrows_4\":0,\"chain_1\":0,\"lipstick_4\":0,\"bproof_2\":0,\"hair_color_1\":0,\"decals_2\":0,\"pants_2\":4,\"age_2\":0,\"glasses_2\":0,\"ears_2\":0,\"arms\":11,\"lipstick_1\":0,\"ears_1\":-1,\"mask_2\":0,\"sex\":0,\"lipstick_3\":0,\"helmet_1\":-1,\"shoes_2\":0,\"beard_2\":0,\"beard_1\":0,\"lipstick_2\":0,\"beard_4\":0,\"glasses_1\":0,\"bproof_1\":0,\"mask_1\":0,\"decals_1\":0,\"hair_1\":0,\"eyebrows_2\":0,\"beard_3\":0,\"age_1\":0,\"tshirt_2\":0,\"skin\":0,\"torso_2\":0,\"eyebrows_1\":0,\"face\":0,\"shoes_1\":10,\"pants_1\":24}', '{\"hair_2\":0,\"hair_color_2\":0,\"torso_1\":57,\"bags_1\":0,\"helmet_2\":0,\"chain_2\":0,\"eyebrows_3\":0,\"makeup_3\":0,\"makeup_2\":0,\"tshirt_1\":38,\"makeup_1\":0,\"bags_2\":0,\"makeup_4\":0,\"eyebrows_4\":0,\"chain_1\":0,\"lipstick_4\":0,\"bproof_2\":0,\"hair_color_1\":0,\"decals_2\":0,\"pants_2\":1,\"age_2\":0,\"glasses_2\":0,\"ears_2\":0,\"arms\":21,\"lipstick_1\":0,\"ears_1\":-1,\"mask_2\":0,\"sex\":1,\"lipstick_3\":0,\"helmet_1\":-1,\"shoes_2\":0,\"beard_2\":0,\"beard_1\":0,\"lipstick_2\":0,\"beard_4\":0,\"glasses_1\":5,\"bproof_1\":0,\"mask_1\":0,\"decals_1\":1,\"hair_1\":0,\"eyebrows_2\":0,\"beard_3\":0,\"age_1\":0,\"tshirt_2\":0,\"skin\":0,\"torso_2\":0,\"eyebrows_1\":0,\"face\":0,\"shoes_1\":49,\"pants_1\":11}');
INSERT INTO `job_grades` VALUES (16, 'taxi', 3, 'uber', 'Uber', 48, '{\"hair_2\":0,\"hair_color_2\":0,\"torso_1\":26,\"bags_1\":0,\"helmet_2\":0,\"chain_2\":0,\"eyebrows_3\":0,\"makeup_3\":0,\"makeup_2\":0,\"tshirt_1\":57,\"makeup_1\":0,\"bags_2\":0,\"makeup_4\":0,\"eyebrows_4\":0,\"chain_1\":0,\"lipstick_4\":0,\"bproof_2\":0,\"hair_color_1\":0,\"decals_2\":0,\"pants_2\":4,\"age_2\":0,\"glasses_2\":0,\"ears_2\":0,\"arms\":11,\"lipstick_1\":0,\"ears_1\":-1,\"mask_2\":0,\"sex\":0,\"lipstick_3\":0,\"helmet_1\":-1,\"shoes_2\":0,\"beard_2\":0,\"beard_1\":0,\"lipstick_2\":0,\"beard_4\":0,\"glasses_1\":0,\"bproof_1\":0,\"mask_1\":0,\"decals_1\":0,\"hair_1\":0,\"eyebrows_2\":0,\"beard_3\":0,\"age_1\":0,\"tshirt_2\":0,\"skin\":0,\"torso_2\":0,\"eyebrows_1\":0,\"face\":0,\"shoes_1\":10,\"pants_1\":24}', '{\"hair_2\":0,\"hair_color_2\":0,\"torso_1\":57,\"bags_1\":0,\"helmet_2\":0,\"chain_2\":0,\"eyebrows_3\":0,\"makeup_3\":0,\"makeup_2\":0,\"tshirt_1\":38,\"makeup_1\":0,\"bags_2\":0,\"makeup_4\":0,\"eyebrows_4\":0,\"chain_1\":0,\"lipstick_4\":0,\"bproof_2\":0,\"hair_color_1\":0,\"decals_2\":0,\"pants_2\":1,\"age_2\":0,\"glasses_2\":0,\"ears_2\":0,\"arms\":21,\"lipstick_1\":0,\"ears_1\":-1,\"mask_2\":0,\"sex\":1,\"lipstick_3\":0,\"helmet_1\":-1,\"shoes_2\":0,\"beard_2\":0,\"beard_1\":0,\"lipstick_2\":0,\"beard_4\":0,\"glasses_1\":5,\"bproof_1\":0,\"mask_1\":0,\"decals_1\":1,\"hair_1\":0,\"eyebrows_2\":0,\"beard_3\":0,\"age_1\":0,\"tshirt_2\":0,\"skin\":0,\"torso_2\":0,\"eyebrows_1\":0,\"face\":0,\"shoes_1\":49,\"pants_1\":11}');
INSERT INTO `job_grades` VALUES (17, 'taxi', 4, 'boss', 'Patrão', 0, '{\"hair_2\":0,\"hair_color_2\":0,\"torso_1\":29,\"bags_1\":0,\"helmet_2\":0,\"chain_2\":0,\"eyebrows_3\":0,\"makeup_3\":0,\"makeup_2\":0,\"tshirt_1\":31,\"makeup_1\":0,\"bags_2\":0,\"makeup_4\":0,\"eyebrows_4\":0,\"chain_1\":0,\"lipstick_4\":0,\"bproof_2\":0,\"hair_color_1\":0,\"decals_2\":0,\"pants_2\":4,\"age_2\":0,\"glasses_2\":0,\"ears_2\":0,\"arms\":1,\"lipstick_1\":0,\"ears_1\":-1,\"mask_2\":0,\"sex\":0,\"lipstick_3\":0,\"helmet_1\":-1,\"shoes_2\":0,\"beard_2\":0,\"beard_1\":0,\"lipstick_2\":0,\"beard_4\":0,\"glasses_1\":0,\"bproof_1\":0,\"mask_1\":0,\"decals_1\":0,\"hair_1\":0,\"eyebrows_2\":0,\"beard_3\":0,\"age_1\":0,\"tshirt_2\":0,\"skin\":0,\"torso_2\":4,\"eyebrows_1\":0,\"face\":0,\"shoes_1\":10,\"pants_1\":24}', '{\"hair_2\":0,\"hair_color_2\":0,\"torso_1\":57,\"bags_1\":0,\"helmet_2\":0,\"chain_2\":0,\"eyebrows_3\":0,\"makeup_3\":0,\"makeup_2\":0,\"tshirt_1\":38,\"makeup_1\":0,\"bags_2\":0,\"makeup_4\":0,\"eyebrows_4\":0,\"chain_1\":0,\"lipstick_4\":0,\"bproof_2\":0,\"hair_color_1\":0,\"decals_2\":0,\"pants_2\":1,\"age_2\":0,\"glasses_2\":0,\"ears_2\":0,\"arms\":21,\"lipstick_1\":0,\"ears_1\":-1,\"mask_2\":0,\"sex\":1,\"lipstick_3\":0,\"helmet_1\":-1,\"shoes_2\":0,\"beard_2\":0,\"beard_1\":0,\"lipstick_2\":0,\"beard_4\":0,\"glasses_1\":5,\"bproof_1\":0,\"mask_1\":0,\"decals_1\":1,\"hair_1\":0,\"eyebrows_2\":0,\"beard_3\":0,\"age_1\":0,\"tshirt_2\":0,\"skin\":0,\"torso_2\":0,\"eyebrows_1\":0,\"face\":0,\"shoes_1\":49,\"pants_1\":11}');
INSERT INTO `job_grades` VALUES (18, 'realestateagent', 0, 'location', 'Locação', 10, '{}', '{}');
INSERT INTO `job_grades` VALUES (19, 'realestateagent', 1, 'vendeur', 'Vendedor', 25, '{}', '{}');
INSERT INTO `job_grades` VALUES (20, 'realestateagent', 2, 'gestion', 'Gestão', 40, '{}', '{}');
INSERT INTO `job_grades` VALUES (21, 'realestateagent', 3, 'boss', 'Patrão', 0, '{}', '{}');
INSERT INTO `job_grades` VALUES (22, 'police', 0, 'recruit', 'Recruta', 20, '{}', '{}');
INSERT INTO `job_grades` VALUES (23, 'police', 1, 'officer', 'Oficial', 40, '{}', '{}');
INSERT INTO `job_grades` VALUES (24, 'police', 2, 'sergeant', 'Sargento', 60, '{}', '{}');
INSERT INTO `job_grades` VALUES (25, 'police', 3, 'lieutenant', 'Tenente', 85, '{}', '{}');
INSERT INTO `job_grades` VALUES (26, 'police', 4, 'boss', 'Comandante', 100, '{}', '{}');
INSERT INTO `job_grades` VALUES (27, 'mechanic', 0, 'recrue', 'Recruta', 12, '{}', '{}');
INSERT INTO `job_grades` VALUES (28, 'mechanic', 1, 'novice', 'Novato', 24, '{}', '{}');
INSERT INTO `job_grades` VALUES (29, 'mechanic', 2, 'experimente', 'Experimente', 36, '{}', '{}');
INSERT INTO `job_grades` VALUES (30, 'mechanic', 3, 'chief', 'Líder da equipe', 48, '{}', '{}');
INSERT INTO `job_grades` VALUES (31, 'mechanic', 4, 'boss', 'Patrão', 0, '{}', '{}');
INSERT INTO `job_grades` VALUES (32, 'banker', 0, 'advisor', 'Assessor', 10, '{}', '{}');
INSERT INTO `job_grades` VALUES (33, 'banker', 1, 'banker', 'Banqueiro', 20, '{}', '{}');
INSERT INTO `job_grades` VALUES (34, 'banker', 2, 'business_banker', 'Negócios banqueiro', 30, '{}', '{}');
INSERT INTO `job_grades` VALUES (35, 'banker', 3, 'trader', 'Comerciante', 40, '{}', '{}');
INSERT INTO `job_grades` VALUES (36, 'banker', 4, 'boss', 'Patrão', 0, '{}', '{}');
INSERT INTO `job_grades` VALUES (37, 'ambulance', 0, 'ambulance', 'ambulância', 20, '{\"tshirt_2\":0,\"hair_color_1\":5,\"glasses_2\":3,\"shoes\":9,\"torso_2\":3,\"hair_color_2\":0,\"pants_1\":24,\"glasses_1\":4,\"hair_1\":2,\"sex\":0,\"decals_2\":0,\"tshirt_1\":15,\"helmet_1\":8,\"helmet_2\":0,\"arms\":92,\"face\":19,\"decals_1\":60,\"torso_1\":13,\"hair_2\":0,\"skin\":34,\"pants_2\":5}', '{\"tshirt_2\":3,\"decals_2\":0,\"glasses\":0,\"hair_1\":2,\"torso_1\":73,\"shoes\":1,\"hair_color_2\":0,\"glasses_1\":19,\"skin\":13,\"face\":6,\"pants_2\":5,\"tshirt_1\":75,\"pants_1\":37,\"helmet_1\":57,\"torso_2\":0,\"arms\":14,\"sex\":1,\"glasses_2\":0,\"decals_1\":0,\"hair_2\":0,\"helmet_2\":0,\"hair_color_1\":0}');
INSERT INTO `job_grades` VALUES (38, 'ambulance', 1, 'doctor', 'médico', 40, '{\"tshirt_2\":0,\"hair_color_1\":5,\"glasses_2\":3,\"shoes\":9,\"torso_2\":3,\"hair_color_2\":0,\"pants_1\":24,\"glasses_1\":4,\"hair_1\":2,\"sex\":0,\"decals_2\":0,\"tshirt_1\":15,\"helmet_1\":8,\"helmet_2\":0,\"arms\":92,\"face\":19,\"decals_1\":60,\"torso_1\":13,\"hair_2\":0,\"skin\":34,\"pants_2\":5}', '{\"tshirt_2\":3,\"decals_2\":0,\"glasses\":0,\"hair_1\":2,\"torso_1\":73,\"shoes\":1,\"hair_color_2\":0,\"glasses_1\":19,\"skin\":13,\"face\":6,\"pants_2\":5,\"tshirt_1\":75,\"pants_1\":37,\"helmet_1\":57,\"torso_2\":0,\"arms\":14,\"sex\":1,\"glasses_2\":0,\"decals_1\":0,\"hair_2\":0,\"helmet_2\":0,\"hair_color_1\":0}');
INSERT INTO `job_grades` VALUES (39, 'ambulance', 2, 'chief_doctor', 'médico chefe', 60, '{\"tshirt_2\":0,\"hair_color_1\":5,\"glasses_2\":3,\"shoes\":9,\"torso_2\":3,\"hair_color_2\":0,\"pants_1\":24,\"glasses_1\":4,\"hair_1\":2,\"sex\":0,\"decals_2\":0,\"tshirt_1\":15,\"helmet_1\":8,\"helmet_2\":0,\"arms\":92,\"face\":19,\"decals_1\":60,\"torso_1\":13,\"hair_2\":0,\"skin\":34,\"pants_2\":5}', '{\"tshirt_2\":3,\"decals_2\":0,\"glasses\":0,\"hair_1\":2,\"torso_1\":73,\"shoes\":1,\"hair_color_2\":0,\"glasses_1\":19,\"skin\":13,\"face\":6,\"pants_2\":5,\"tshirt_1\":75,\"pants_1\":37,\"helmet_1\":57,\"torso_2\":0,\"arms\":14,\"sex\":1,\"glasses_2\":0,\"decals_1\":0,\"hair_2\":0,\"helmet_2\":0,\"hair_color_1\":0}');
INSERT INTO `job_grades` VALUES (40, 'ambulance', 3, 'boss', 'cirurgião', 80, '{\"tshirt_2\":0,\"hair_color_1\":5,\"glasses_2\":3,\"shoes\":9,\"torso_2\":3,\"hair_color_2\":0,\"pants_1\":24,\"glasses_1\":4,\"hair_1\":2,\"sex\":0,\"decals_2\":0,\"tshirt_1\":15,\"helmet_1\":8,\"helmet_2\":0,\"arms\":92,\"face\":19,\"decals_1\":60,\"torso_1\":13,\"hair_2\":0,\"skin\":34,\"pants_2\":5}', '{\"tshirt_2\":3,\"decals_2\":0,\"glasses\":0,\"hair_1\":2,\"torso_1\":73,\"shoes\":1,\"hair_color_2\":0,\"glasses_1\":19,\"skin\":13,\"face\":6,\"pants_2\":5,\"tshirt_1\":75,\"pants_1\":37,\"helmet_1\":57,\"torso_2\":0,\"arms\":14,\"sex\":1,\"glasses_2\":0,\"decals_1\":0,\"hair_2\":0,\"helmet_2\":0,\"hair_color_1\":0}');

-- ----------------------------
-- Table structure for jobs
-- ----------------------------
DROP TABLE IF EXISTS `jobs`;
CREATE TABLE `jobs`  (
  `name` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `label` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `whitelisted` tinyint(1) NOT NULL DEFAULT 0,
  PRIMARY KEY (`name`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of jobs
-- ----------------------------
INSERT INTO `jobs` VALUES ('ambulance', 'Ambulância', 1);
INSERT INTO `jobs` VALUES ('banker', 'Banqueiro', 1);
INSERT INTO `jobs` VALUES ('cardealer', 'Concessionário', 1);
INSERT INTO `jobs` VALUES ('fisherman', 'Pescador', 0);
INSERT INTO `jobs` VALUES ('fueler', 'Refinador', 0);
INSERT INTO `jobs` VALUES ('lumberjack', 'Lenhador', 0);
INSERT INTO `jobs` VALUES ('mechanic', 'Mecânico', 0);
INSERT INTO `jobs` VALUES ('miner', 'Mineiro', 0);
INSERT INTO `jobs` VALUES ('police', 'Policia militar', 1);
INSERT INTO `jobs` VALUES ('realestateagent', 'Agente imobiliário', 0);
INSERT INTO `jobs` VALUES ('reporter', 'Jornalista', 0);
INSERT INTO `jobs` VALUES ('slaughterer', 'Abatedor', 0);
INSERT INTO `jobs` VALUES ('tailor', 'Costureiro', 0);
INSERT INTO `jobs` VALUES ('taxi', 'Taxi', 0);
INSERT INTO `jobs` VALUES ('unemployed', 'Desempregado', 0);

-- ----------------------------
-- Table structure for licenses
-- ----------------------------
DROP TABLE IF EXISTS `licenses`;
CREATE TABLE `licenses`  (
  `type` varchar(55) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `label` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  PRIMARY KEY (`type`) USING BTREE,
  INDEX `type`(`type`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of licenses
-- ----------------------------
INSERT INTO `licenses` VALUES ('boat', 'Licença de barco');
INSERT INTO `licenses` VALUES ('dmv', 'Licença para dirigir');
INSERT INTO `licenses` VALUES ('drive', 'Carteira de motorista');
INSERT INTO `licenses` VALUES ('drive_bike', 'Licença de motocicleta');
INSERT INTO `licenses` VALUES ('drive_truck', 'Licença de motorista comercial');
INSERT INTO `licenses` VALUES ('weapon', 'Licença para portar uma arma');
INSERT INTO `licenses` VALUES ('weed_processing', 'Licença de Processamento de Maconha');

-- ----------------------------
-- Table structure for owned_properties
-- ----------------------------
DROP TABLE IF EXISTS `owned_properties`;
CREATE TABLE `owned_properties`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `price` double NOT NULL,
  `rented` int(11) NOT NULL,
  `owner` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for owned_vehicles
-- ----------------------------
DROP TABLE IF EXISTS `owned_vehicles`;
CREATE TABLE `owned_vehicles`  (
  `owner` varchar(22) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `plate` varchar(12) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `vehicle` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL,
  `type` varchar(20) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL DEFAULT 'car',
  `job` varchar(20) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `stored` tinyint(1) NOT NULL DEFAULT 0,
  PRIMARY KEY (`plate`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for properties
-- ----------------------------
DROP TABLE IF EXISTS `properties`;
CREATE TABLE `properties`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `label` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `entering` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `exit` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `inside` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `outside` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `ipls` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT '[]',
  `gateway` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `is_single` int(11) NULL DEFAULT NULL,
  `is_room` int(11) NULL DEFAULT NULL,
  `is_gateway` int(11) NULL DEFAULT NULL,
  `room_menu` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `price` int(11) NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 73 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of properties
-- ----------------------------
INSERT INTO `properties` VALUES (1, 'WhispymoundDrive', '2677 Whispymound Drive', '{\"y\":564.89,\"z\":182.959,\"x\":119.384}', '{\"x\":117.347,\"y\":559.506,\"z\":183.304}', '{\"y\":557.032,\"z\":183.301,\"x\":118.037}', '{\"y\":567.798,\"z\":182.131,\"x\":119.249}', '[]', NULL, 1, 1, 0, '{\"x\":118.748,\"y\":566.573,\"z\":175.697}', 1500000);
INSERT INTO `properties` VALUES (2, 'NorthConkerAvenue2045', '2045 North Conker Avenue', '{\"x\":372.796,\"y\":428.327,\"z\":144.685}', '{\"x\":373.548,\"y\":422.982,\"z\":144.907},', '{\"y\":420.075,\"z\":145.904,\"x\":372.161}', '{\"x\":372.454,\"y\":432.886,\"z\":143.443}', '[]', NULL, 1, 1, 0, '{\"x\":377.349,\"y\":429.422,\"z\":137.3}', 1500000);
INSERT INTO `properties` VALUES (3, 'RichardMajesticApt2', 'Richard Majestic, Apt 2', '{\"y\":-379.165,\"z\":37.961,\"x\":-936.363}', '{\"y\":-365.476,\"z\":113.274,\"x\":-913.097}', '{\"y\":-367.637,\"z\":113.274,\"x\":-918.022}', '{\"y\":-382.023,\"z\":37.961,\"x\":-943.626}', '[]', NULL, 1, 1, 0, '{\"x\":-927.554,\"y\":-377.744,\"z\":112.674}', 1700000);
INSERT INTO `properties` VALUES (4, 'NorthConkerAvenue2044', '2044 North Conker Avenue', '{\"y\":440.8,\"z\":146.702,\"x\":346.964}', '{\"y\":437.456,\"z\":148.394,\"x\":341.683}', '{\"y\":435.626,\"z\":148.394,\"x\":339.595}', '{\"x\":350.535,\"y\":443.329,\"z\":145.764}', '[]', NULL, 1, 1, 0, '{\"x\":337.726,\"y\":436.985,\"z\":140.77}', 1500000);
INSERT INTO `properties` VALUES (5, 'WildOatsDrive', '3655 Wild Oats Drive', '{\"y\":502.696,\"z\":136.421,\"x\":-176.003}', '{\"y\":497.817,\"z\":136.653,\"x\":-174.349}', '{\"y\":495.069,\"z\":136.666,\"x\":-173.331}', '{\"y\":506.412,\"z\":135.0664,\"x\":-177.927}', '[]', NULL, 1, 1, 0, '{\"x\":-174.725,\"y\":493.095,\"z\":129.043}', 1500000);
INSERT INTO `properties` VALUES (6, 'HillcrestAvenue2862', '2862 Hillcrest Avenue', '{\"y\":596.58,\"z\":142.641,\"x\":-686.554}', '{\"y\":591.988,\"z\":144.392,\"x\":-681.728}', '{\"y\":590.608,\"z\":144.392,\"x\":-680.124}', '{\"y\":599.019,\"z\":142.059,\"x\":-689.492}', '[]', NULL, 1, 1, 0, '{\"x\":-680.46,\"y\":588.6,\"z\":136.769}', 1500000);
INSERT INTO `properties` VALUES (7, 'LowEndApartment', 'Appartement de base', '{\"y\":-1078.735,\"z\":28.4031,\"x\":292.528}', '{\"y\":-1007.152,\"z\":-102.002,\"x\":265.845}', '{\"y\":-1002.802,\"z\":-100.008,\"x\":265.307}', '{\"y\":-1078.669,\"z\":28.401,\"x\":296.738}', '[]', NULL, 1, 1, 0, '{\"x\":265.916,\"y\":-999.38,\"z\":-100.008}', 562500);
INSERT INTO `properties` VALUES (8, 'MadWayneThunder', '2113 Mad Wayne Thunder', '{\"y\":454.955,\"z\":96.462,\"x\":-1294.433}', '{\"x\":-1289.917,\"y\":449.541,\"z\":96.902}', '{\"y\":446.322,\"z\":96.899,\"x\":-1289.642}', '{\"y\":455.453,\"z\":96.517,\"x\":-1298.851}', '[]', NULL, 1, 1, 0, '{\"x\":-1287.306,\"y\":455.901,\"z\":89.294}', 1500000);
INSERT INTO `properties` VALUES (9, 'HillcrestAvenue2874', '2874 Hillcrest Avenue', '{\"x\":-853.346,\"y\":696.678,\"z\":147.782}', '{\"y\":690.875,\"z\":151.86,\"x\":-859.961}', '{\"y\":688.361,\"z\":151.857,\"x\":-859.395}', '{\"y\":701.628,\"z\":147.773,\"x\":-855.007}', '[]', NULL, 1, 1, 0, '{\"x\":-858.543,\"y\":697.514,\"z\":144.253}', 1500000);
INSERT INTO `properties` VALUES (10, 'HillcrestAvenue2868', '2868 Hillcrest Avenue', '{\"y\":620.494,\"z\":141.588,\"x\":-752.82}', '{\"y\":618.62,\"z\":143.153,\"x\":-759.317}', '{\"y\":617.629,\"z\":143.153,\"x\":-760.789}', '{\"y\":621.281,\"z\":141.254,\"x\":-750.919}', '[]', NULL, 1, 1, 0, '{\"x\":-762.504,\"y\":618.992,\"z\":135.53}', 1500000);
INSERT INTO `properties` VALUES (11, 'TinselTowersApt12', 'Tinsel Towers, Apt 42', '{\"y\":37.025,\"z\":42.58,\"x\":-618.299}', '{\"y\":58.898,\"z\":97.2,\"x\":-603.301}', '{\"y\":58.941,\"z\":97.2,\"x\":-608.741}', '{\"y\":30.603,\"z\":42.524,\"x\":-620.017}', '[]', NULL, 1, 1, 0, '{\"x\":-622.173,\"y\":54.585,\"z\":96.599}', 1700000);
INSERT INTO `properties` VALUES (12, 'MiltonDrive', 'Milton Drive', '{\"x\":-775.17,\"y\":312.01,\"z\":84.658}', NULL, NULL, '{\"x\":-775.346,\"y\":306.776,\"z\":84.7}', '[]', NULL, 0, 0, 1, NULL, 0);
INSERT INTO `properties` VALUES (13, 'Modern1Apartment', 'Appartement Moderne 1', NULL, '{\"x\":-784.194,\"y\":323.636,\"z\":210.997}', '{\"x\":-779.751,\"y\":323.385,\"z\":210.997}', NULL, '[\"apa_v_mp_h_01_a\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-766.661,\"y\":327.672,\"z\":210.396}', 1300000);
INSERT INTO `properties` VALUES (14, 'Modern2Apartment', 'Appartement Moderne 2', NULL, '{\"x\":-786.8663,\"y\":315.764,\"z\":186.913}', '{\"x\":-781.808,\"y\":315.866,\"z\":186.913}', NULL, '[\"apa_v_mp_h_01_c\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-795.735,\"y\":326.757,\"z\":186.313}', 1300000);
INSERT INTO `properties` VALUES (15, 'Modern3Apartment', 'Appartement Moderne 3', NULL, '{\"x\":-774.012,\"y\":342.042,\"z\":195.686}', '{\"x\":-779.057,\"y\":342.063,\"z\":195.686}', NULL, '[\"apa_v_mp_h_01_b\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-765.386,\"y\":330.782,\"z\":195.08}', 1300000);
INSERT INTO `properties` VALUES (16, 'Mody1Apartment', 'Appartement Mode 1', NULL, '{\"x\":-784.194,\"y\":323.636,\"z\":210.997}', '{\"x\":-779.751,\"y\":323.385,\"z\":210.997}', NULL, '[\"apa_v_mp_h_02_a\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-766.615,\"y\":327.878,\"z\":210.396}', 1300000);
INSERT INTO `properties` VALUES (17, 'Mody2Apartment', 'Appartement Mode 2', NULL, '{\"x\":-786.8663,\"y\":315.764,\"z\":186.913}', '{\"x\":-781.808,\"y\":315.866,\"z\":186.913}', NULL, '[\"apa_v_mp_h_02_c\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-795.297,\"y\":327.092,\"z\":186.313}', 1300000);
INSERT INTO `properties` VALUES (18, 'Mody3Apartment', 'Appartement Mode 3', NULL, '{\"x\":-774.012,\"y\":342.042,\"z\":195.686}', '{\"x\":-779.057,\"y\":342.063,\"z\":195.686}', NULL, '[\"apa_v_mp_h_02_b\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-765.303,\"y\":330.932,\"z\":195.085}', 1300000);
INSERT INTO `properties` VALUES (19, 'Vibrant1Apartment', 'Appartement Vibrant 1', NULL, '{\"x\":-784.194,\"y\":323.636,\"z\":210.997}', '{\"x\":-779.751,\"y\":323.385,\"z\":210.997}', NULL, '[\"apa_v_mp_h_03_a\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-765.885,\"y\":327.641,\"z\":210.396}', 1300000);
INSERT INTO `properties` VALUES (20, 'Vibrant2Apartment', 'Appartement Vibrant 2', NULL, '{\"x\":-786.8663,\"y\":315.764,\"z\":186.913}', '{\"x\":-781.808,\"y\":315.866,\"z\":186.913}', NULL, '[\"apa_v_mp_h_03_c\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-795.607,\"y\":327.344,\"z\":186.313}', 1300000);
INSERT INTO `properties` VALUES (21, 'Vibrant3Apartment', 'Appartement Vibrant 3', NULL, '{\"x\":-774.012,\"y\":342.042,\"z\":195.686}', '{\"x\":-779.057,\"y\":342.063,\"z\":195.686}', NULL, '[\"apa_v_mp_h_03_b\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-765.525,\"y\":330.851,\"z\":195.085}', 1300000);
INSERT INTO `properties` VALUES (22, 'Sharp1Apartment', 'Appartement Persan 1', NULL, '{\"x\":-784.194,\"y\":323.636,\"z\":210.997}', '{\"x\":-779.751,\"y\":323.385,\"z\":210.997}', NULL, '[\"apa_v_mp_h_04_a\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-766.527,\"y\":327.89,\"z\":210.396}', 1300000);
INSERT INTO `properties` VALUES (23, 'Sharp2Apartment', 'Appartement Persan 2', NULL, '{\"x\":-786.8663,\"y\":315.764,\"z\":186.913}', '{\"x\":-781.808,\"y\":315.866,\"z\":186.913}', NULL, '[\"apa_v_mp_h_04_c\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-795.642,\"y\":326.497,\"z\":186.313}', 1300000);
INSERT INTO `properties` VALUES (24, 'Sharp3Apartment', 'Appartement Persan 3', NULL, '{\"x\":-774.012,\"y\":342.042,\"z\":195.686}', '{\"x\":-779.057,\"y\":342.063,\"z\":195.686}', NULL, '[\"apa_v_mp_h_04_b\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-765.503,\"y\":331.318,\"z\":195.085}', 1300000);
INSERT INTO `properties` VALUES (25, 'Monochrome1Apartment', 'Appartement Monochrome 1', NULL, '{\"x\":-784.194,\"y\":323.636,\"z\":210.997}', '{\"x\":-779.751,\"y\":323.385,\"z\":210.997}', NULL, '[\"apa_v_mp_h_05_a\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-766.289,\"y\":328.086,\"z\":210.396}', 1300000);
INSERT INTO `properties` VALUES (26, 'Monochrome2Apartment', 'Appartement Monochrome 2', NULL, '{\"x\":-786.8663,\"y\":315.764,\"z\":186.913}', '{\"x\":-781.808,\"y\":315.866,\"z\":186.913}', NULL, '[\"apa_v_mp_h_05_c\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-795.692,\"y\":326.762,\"z\":186.313}', 1300000);
INSERT INTO `properties` VALUES (27, 'Monochrome3Apartment', 'Appartement Monochrome 3', NULL, '{\"x\":-774.012,\"y\":342.042,\"z\":195.686}', '{\"x\":-779.057,\"y\":342.063,\"z\":195.686}', NULL, '[\"apa_v_mp_h_05_b\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-765.094,\"y\":330.976,\"z\":195.085}', 1300000);
INSERT INTO `properties` VALUES (28, 'Seductive1Apartment', 'Appartement Séduisant 1', NULL, '{\"x\":-784.194,\"y\":323.636,\"z\":210.997}', '{\"x\":-779.751,\"y\":323.385,\"z\":210.997}', NULL, '[\"apa_v_mp_h_06_a\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-766.263,\"y\":328.104,\"z\":210.396}', 1300000);
INSERT INTO `properties` VALUES (29, 'Seductive2Apartment', 'Appartement Séduisant 2', NULL, '{\"x\":-786.8663,\"y\":315.764,\"z\":186.913}', '{\"x\":-781.808,\"y\":315.866,\"z\":186.913}', NULL, '[\"apa_v_mp_h_06_c\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-795.655,\"y\":326.611,\"z\":186.313}', 1300000);
INSERT INTO `properties` VALUES (30, 'Seductive3Apartment', 'Appartement Séduisant 3', NULL, '{\"x\":-774.012,\"y\":342.042,\"z\":195.686}', '{\"x\":-779.057,\"y\":342.063,\"z\":195.686}', NULL, '[\"apa_v_mp_h_06_b\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-765.3,\"y\":331.414,\"z\":195.085}', 1300000);
INSERT INTO `properties` VALUES (31, 'Regal1Apartment', 'Appartement Régal 1', NULL, '{\"x\":-784.194,\"y\":323.636,\"z\":210.997}', '{\"x\":-779.751,\"y\":323.385,\"z\":210.997}', NULL, '[\"apa_v_mp_h_07_a\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-765.956,\"y\":328.257,\"z\":210.396}', 1300000);
INSERT INTO `properties` VALUES (32, 'Regal2Apartment', 'Appartement Régal 2', NULL, '{\"x\":-786.8663,\"y\":315.764,\"z\":186.913}', '{\"x\":-781.808,\"y\":315.866,\"z\":186.913}', NULL, '[\"apa_v_mp_h_07_c\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-795.545,\"y\":326.659,\"z\":186.313}', 1300000);
INSERT INTO `properties` VALUES (33, 'Regal3Apartment', 'Appartement Régal 3', NULL, '{\"x\":-774.012,\"y\":342.042,\"z\":195.686}', '{\"x\":-779.057,\"y\":342.063,\"z\":195.686}', NULL, '[\"apa_v_mp_h_07_b\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-765.087,\"y\":331.429,\"z\":195.123}', 1300000);
INSERT INTO `properties` VALUES (34, 'Aqua1Apartment', 'Appartement Aqua 1', NULL, '{\"x\":-784.194,\"y\":323.636,\"z\":210.997}', '{\"x\":-779.751,\"y\":323.385,\"z\":210.997}', NULL, '[\"apa_v_mp_h_08_a\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-766.187,\"y\":328.47,\"z\":210.396}', 1300000);
INSERT INTO `properties` VALUES (35, 'Aqua2Apartment', 'Appartement Aqua 2', NULL, '{\"x\":-786.8663,\"y\":315.764,\"z\":186.913}', '{\"x\":-781.808,\"y\":315.866,\"z\":186.913}', NULL, '[\"apa_v_mp_h_08_c\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-795.658,\"y\":326.563,\"z\":186.313}', 1300000);
INSERT INTO `properties` VALUES (36, 'Aqua3Apartment', 'Appartement Aqua 3', NULL, '{\"x\":-774.012,\"y\":342.042,\"z\":195.686}', '{\"x\":-779.057,\"y\":342.063,\"z\":195.686}', NULL, '[\"apa_v_mp_h_08_b\"]', 'MiltonDrive', 0, 1, 0, '{\"x\":-765.287,\"y\":331.084,\"z\":195.086}', 1300000);
INSERT INTO `properties` VALUES (37, 'IntegrityWay', '4 Integrity Way', '{\"x\":-47.804,\"y\":-585.867,\"z\":36.956}', NULL, NULL, '{\"x\":-54.178,\"y\":-583.762,\"z\":35.798}', '[]', NULL, 0, 0, 1, NULL, 0);
INSERT INTO `properties` VALUES (38, 'IntegrityWay28', '4 Integrity Way - Apt 28', NULL, '{\"x\":-31.409,\"y\":-594.927,\"z\":79.03}', '{\"x\":-26.098,\"y\":-596.909,\"z\":79.03}', NULL, '[]', 'IntegrityWay', 0, 1, 0, '{\"x\":-11.923,\"y\":-597.083,\"z\":78.43}', 1700000);
INSERT INTO `properties` VALUES (39, 'IntegrityWay30', '4 Integrity Way - Apt 30', NULL, '{\"x\":-17.702,\"y\":-588.524,\"z\":89.114}', '{\"x\":-16.21,\"y\":-582.569,\"z\":89.114}', NULL, '[]', 'IntegrityWay', 0, 1, 0, '{\"x\":-26.327,\"y\":-588.384,\"z\":89.123}', 1700000);
INSERT INTO `properties` VALUES (40, 'DellPerroHeights', 'Dell Perro Heights', '{\"x\":-1447.06,\"y\":-538.28,\"z\":33.74}', NULL, NULL, '{\"x\":-1440.022,\"y\":-548.696,\"z\":33.74}', '[]', NULL, 0, 0, 1, NULL, 0);
INSERT INTO `properties` VALUES (41, 'DellPerroHeightst4', 'Dell Perro Heights - Apt 28', NULL, '{\"x\":-1452.125,\"y\":-540.591,\"z\":73.044}', '{\"x\":-1455.435,\"y\":-535.79,\"z\":73.044}', NULL, '[]', 'DellPerroHeights', 0, 1, 0, '{\"x\":-1467.058,\"y\":-527.571,\"z\":72.443}', 1700000);
INSERT INTO `properties` VALUES (42, 'DellPerroHeightst7', 'Dell Perro Heights - Apt 30', NULL, '{\"x\":-1451.562,\"y\":-523.535,\"z\":55.928}', '{\"x\":-1456.02,\"y\":-519.209,\"z\":55.929}', NULL, '[]', 'DellPerroHeights', 0, 1, 0, '{\"x\":-1457.026,\"y\":-530.219,\"z\":55.937}', 1700000);
INSERT INTO `properties` VALUES (43, 'MazeBankBuilding', 'Maze Bank Building', '{\"x\":-79.18,\"y\":-795.92,\"z\":43.35}', NULL, NULL, '{\"x\":-72.50,\"y\":-786.92,\"z\":43.40}', '[]', NULL, 0, 0, 1, NULL, 0);
INSERT INTO `properties` VALUES (44, 'OldSpiceWarm', 'Old Spice Warm', NULL, '{\"x\":-75.69,\"y\":-827.08,\"z\":242.43}', '{\"x\":-75.51,\"y\":-823.90,\"z\":242.43}', NULL, '[\"ex_dt1_11_office_01a\"]', 'MazeBankBuilding', 0, 1, 0, '{\"x\":-71.81,\"y\":-814.34,\"z\":242.39}', 5000000);
INSERT INTO `properties` VALUES (45, 'OldSpiceClassical', 'Old Spice Classical', NULL, '{\"x\":-75.69,\"y\":-827.08,\"z\":242.43}', '{\"x\":-75.51,\"y\":-823.90,\"z\":242.43}', NULL, '[\"ex_dt1_11_office_01b\"]', 'MazeBankBuilding', 0, 1, 0, '{\"x\":-71.81,\"y\":-814.34,\"z\":242.39}', 5000000);
INSERT INTO `properties` VALUES (46, 'OldSpiceVintage', 'Old Spice Vintage', NULL, '{\"x\":-75.69,\"y\":-827.08,\"z\":242.43}', '{\"x\":-75.51,\"y\":-823.90,\"z\":242.43}', NULL, '[\"ex_dt1_11_office_01c\"]', 'MazeBankBuilding', 0, 1, 0, '{\"x\":-71.81,\"y\":-814.34,\"z\":242.39}', 5000000);
INSERT INTO `properties` VALUES (47, 'ExecutiveRich', 'Executive Rich', NULL, '{\"x\":-75.69,\"y\":-827.08,\"z\":242.43}', '{\"x\":-75.51,\"y\":-823.90,\"z\":242.43}', NULL, '[\"ex_dt1_11_office_02b\"]', 'MazeBankBuilding', 0, 1, 0, '{\"x\":-71.81,\"y\":-814.34,\"z\":242.39}', 5000000);
INSERT INTO `properties` VALUES (48, 'ExecutiveCool', 'Executive Cool', NULL, '{\"x\":-75.69,\"y\":-827.08,\"z\":242.43}', '{\"x\":-75.51,\"y\":-823.90,\"z\":242.43}', NULL, '[\"ex_dt1_11_office_02c\"]', 'MazeBankBuilding', 0, 1, 0, '{\"x\":-71.81,\"y\":-814.34,\"z\":242.39}', 5000000);
INSERT INTO `properties` VALUES (49, 'ExecutiveContrast', 'Executive Contrast', NULL, '{\"x\":-75.69,\"y\":-827.08,\"z\":242.43}', '{\"x\":-75.51,\"y\":-823.90,\"z\":242.43}', NULL, '[\"ex_dt1_11_office_02a\"]', 'MazeBankBuilding', 0, 1, 0, '{\"x\":-71.81,\"y\":-814.34,\"z\":242.39}', 5000000);
INSERT INTO `properties` VALUES (50, 'PowerBrokerIce', 'Power Broker Ice', NULL, '{\"x\":-75.69,\"y\":-827.08,\"z\":242.43}', '{\"x\":-75.51,\"y\":-823.90,\"z\":242.43}', NULL, '[\"ex_dt1_11_office_03a\"]', 'MazeBankBuilding', 0, 1, 0, '{\"x\":-71.81,\"y\":-814.34,\"z\":242.39}', 5000000);
INSERT INTO `properties` VALUES (51, 'PowerBrokerConservative', 'Power Broker Conservative', NULL, '{\"x\":-75.69,\"y\":-827.08,\"z\":242.43}', '{\"x\":-75.51,\"y\":-823.90,\"z\":242.43}', NULL, '[\"ex_dt1_11_office_03b\"]', 'MazeBankBuilding', 0, 1, 0, '{\"x\":-71.81,\"y\":-814.34,\"z\":242.39}', 5000000);
INSERT INTO `properties` VALUES (52, 'PowerBrokerPolished', 'Power Broker Polished', NULL, '{\"x\":-75.69,\"y\":-827.08,\"z\":242.43}', '{\"x\":-75.51,\"y\":-823.90,\"z\":242.43}', NULL, '[\"ex_dt1_11_office_03c\"]', 'MazeBankBuilding', 0, 1, 0, '{\"x\":-71.81,\"y\":-814.34,\"z\":242.39}', 5000000);
INSERT INTO `properties` VALUES (53, 'LomBank', 'Lom Bank', '{\"x\":-1581.36,\"y\":-558.23,\"z\":34.07}', NULL, NULL, '{\"x\":-1583.60,\"y\":-555.12,\"z\":34.07}', '[]', NULL, 0, 0, 1, NULL, 0);
INSERT INTO `properties` VALUES (54, 'LBOldSpiceWarm', 'LB Old Spice Warm', NULL, '{\"x\":-1579.53,\"y\":-564.89,\"z\":107.62}', '{\"x\":-1576.42,\"y\":-567.57,\"z\":107.62}', NULL, '[\"ex_sm_13_office_01a\"]', 'LomBank', 0, 1, 0, '{\"x\":-1571.26,\"y\":-575.76,\"z\":107.52}', 3500000);
INSERT INTO `properties` VALUES (55, 'LBOldSpiceClassical', 'LB Old Spice Classical', NULL, '{\"x\":-1579.53,\"y\":-564.89,\"z\":107.62}', '{\"x\":-1576.42,\"y\":-567.57,\"z\":107.62}', NULL, '[\"ex_sm_13_office_01b\"]', 'LomBank', 0, 1, 0, '{\"x\":-1571.26,\"y\":-575.76,\"z\":107.52}', 3500000);
INSERT INTO `properties` VALUES (56, 'LBOldSpiceVintage', 'LB Old Spice Vintage', NULL, '{\"x\":-1579.53,\"y\":-564.89,\"z\":107.62}', '{\"x\":-1576.42,\"y\":-567.57,\"z\":107.62}', NULL, '[\"ex_sm_13_office_01c\"]', 'LomBank', 0, 1, 0, '{\"x\":-1571.26,\"y\":-575.76,\"z\":107.52}', 3500000);
INSERT INTO `properties` VALUES (57, 'LBExecutiveRich', 'LB Executive Rich', NULL, '{\"x\":-1579.53,\"y\":-564.89,\"z\":107.62}', '{\"x\":-1576.42,\"y\":-567.57,\"z\":107.62}', NULL, '[\"ex_sm_13_office_02b\"]', 'LomBank', 0, 1, 0, '{\"x\":-1571.26,\"y\":-575.76,\"z\":107.52}', 3500000);
INSERT INTO `properties` VALUES (58, 'LBExecutiveCool', 'LB Executive Cool', NULL, '{\"x\":-1579.53,\"y\":-564.89,\"z\":107.62}', '{\"x\":-1576.42,\"y\":-567.57,\"z\":107.62}', NULL, '[\"ex_sm_13_office_02c\"]', 'LomBank', 0, 1, 0, '{\"x\":-1571.26,\"y\":-575.76,\"z\":107.52}', 3500000);
INSERT INTO `properties` VALUES (59, 'LBExecutiveContrast', 'LB Executive Contrast', NULL, '{\"x\":-1579.53,\"y\":-564.89,\"z\":107.62}', '{\"x\":-1576.42,\"y\":-567.57,\"z\":107.62}', NULL, '[\"ex_sm_13_office_02a\"]', 'LomBank', 0, 1, 0, '{\"x\":-1571.26,\"y\":-575.76,\"z\":107.52}', 3500000);
INSERT INTO `properties` VALUES (60, 'LBPowerBrokerIce', 'LB Power Broker Ice', NULL, '{\"x\":-1579.53,\"y\":-564.89,\"z\":107.62}', '{\"x\":-1576.42,\"y\":-567.57,\"z\":107.62}', NULL, '[\"ex_sm_13_office_03a\"]', 'LomBank', 0, 1, 0, '{\"x\":-1571.26,\"y\":-575.76,\"z\":107.52}', 3500000);
INSERT INTO `properties` VALUES (61, 'LBPowerBrokerConservative', 'LB Power Broker Conservative', NULL, '{\"x\":-1579.53,\"y\":-564.89,\"z\":107.62}', '{\"x\":-1576.42,\"y\":-567.57,\"z\":107.62}', NULL, '[\"ex_sm_13_office_03b\"]', 'LomBank', 0, 1, 0, '{\"x\":-1571.26,\"y\":-575.76,\"z\":107.52}', 3500000);
INSERT INTO `properties` VALUES (62, 'LBPowerBrokerPolished', 'LB Power Broker Polished', NULL, '{\"x\":-1579.53,\"y\":-564.89,\"z\":107.62}', '{\"x\":-1576.42,\"y\":-567.57,\"z\":107.62}', NULL, '[\"ex_sm_13_office_03c\"]', 'LomBank', 0, 1, 0, '{\"x\":-1571.26,\"y\":-575.76,\"z\":107.52}', 3500000);
INSERT INTO `properties` VALUES (63, 'MazeBankWest', 'Maze Bank West', '{\"x\":-1379.58,\"y\":-499.63,\"z\":32.22}', NULL, NULL, '{\"x\":-1378.95,\"y\":-502.82,\"z\":32.22}', '[]', NULL, 0, 0, 1, NULL, 0);
INSERT INTO `properties` VALUES (64, 'MBWOldSpiceWarm', 'MBW Old Spice Warm', NULL, '{\"x\":-1392.74,\"y\":-480.18,\"z\":71.14}', '{\"x\":-1389.43,\"y\":-479.01,\"z\":71.14}', NULL, '[\"ex_sm_15_office_01a\"]', 'MazeBankWest', 0, 1, 0, '{\"x\":-1390.76,\"y\":-479.22,\"z\":72.04}', 2700000);
INSERT INTO `properties` VALUES (65, 'MBWOldSpiceClassical', 'MBW Old Spice Classical', NULL, '{\"x\":-1392.74,\"y\":-480.18,\"z\":71.14}', '{\"x\":-1389.43,\"y\":-479.01,\"z\":71.14}', NULL, '[\"ex_sm_15_office_01b\"]', 'MazeBankWest', 0, 1, 0, '{\"x\":-1390.76,\"y\":-479.22,\"z\":72.04}', 2700000);
INSERT INTO `properties` VALUES (66, 'MBWOldSpiceVintage', 'MBW Old Spice Vintage', NULL, '{\"x\":-1392.74,\"y\":-480.18,\"z\":71.14}', '{\"x\":-1389.43,\"y\":-479.01,\"z\":71.14}', NULL, '[\"ex_sm_15_office_01c\"]', 'MazeBankWest', 0, 1, 0, '{\"x\":-1390.76,\"y\":-479.22,\"z\":72.04}', 2700000);
INSERT INTO `properties` VALUES (67, 'MBWExecutiveRich', 'MBW Executive Rich', NULL, '{\"x\":-1392.74,\"y\":-480.18,\"z\":71.14}', '{\"x\":-1389.43,\"y\":-479.01,\"z\":71.14}', NULL, '[\"ex_sm_15_office_02b\"]', 'MazeBankWest', 0, 1, 0, '{\"x\":-1390.76,\"y\":-479.22,\"z\":72.04}', 2700000);
INSERT INTO `properties` VALUES (68, 'MBWExecutiveCool', 'MBW Executive Cool', NULL, '{\"x\":-1392.74,\"y\":-480.18,\"z\":71.14}', '{\"x\":-1389.43,\"y\":-479.01,\"z\":71.14}', NULL, '[\"ex_sm_15_office_02c\"]', 'MazeBankWest', 0, 1, 0, '{\"x\":-1390.76,\"y\":-479.22,\"z\":72.04}', 2700000);
INSERT INTO `properties` VALUES (69, 'MBWExecutive Contrast', 'MBW Executive Contrast', NULL, '{\"x\":-1392.74,\"y\":-480.18,\"z\":71.14}', '{\"x\":-1389.43,\"y\":-479.01,\"z\":71.14}', NULL, '[\"ex_sm_15_office_02a\"]', 'MazeBankWest', 0, 1, 0, '{\"x\":-1390.76,\"y\":-479.22,\"z\":72.04}', 2700000);
INSERT INTO `properties` VALUES (70, 'MBWPowerBrokerIce', 'MBW Power Broker Ice', NULL, '{\"x\":-1392.74,\"y\":-480.18,\"z\":71.14}', '{\"x\":-1389.43,\"y\":-479.01,\"z\":71.14}', NULL, '[\"ex_sm_15_office_03a\"]', 'MazeBankWest', 0, 1, 0, '{\"x\":-1390.76,\"y\":-479.22,\"z\":72.04}', 2700000);
INSERT INTO `properties` VALUES (71, 'MBWPowerBrokerConvservative', 'MBW Power Broker Convservative', NULL, '{\"x\":-1392.74,\"y\":-480.18,\"z\":71.14}', '{\"x\":-1389.43,\"y\":-479.01,\"z\":71.14}', NULL, '[\"ex_sm_15_office_03b\"]', 'MazeBankWest', 0, 1, 0, '{\"x\":-1390.76,\"y\":-479.22,\"z\":72.04}', 2700000);
INSERT INTO `properties` VALUES (72, 'MBWPowerBrokerPolished', 'MBW Power Broker Polished', NULL, '{\"x\":-1392.74,\"y\":-480.18,\"z\":71.14}', '{\"x\":-1389.43,\"y\":-479.01,\"z\":71.14}', NULL, '[\"ex_sm_15_office_03c\"]', 'MazeBankWest', 0, 1, 0, '{\"x\":-1390.76,\"y\":-479.22,\"z\":72.04}', 2700000);

-- ----------------------------
-- Table structure for rented_vehicles
-- ----------------------------
DROP TABLE IF EXISTS `rented_vehicles`;
CREATE TABLE `rented_vehicles`  (
  `vehicle` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `plate` varchar(12) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `player_name` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `base_price` int(11) NOT NULL,
  `rent_price` int(11) NOT NULL,
  `owner` varchar(22) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  PRIMARY KEY (`plate`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for shops
-- ----------------------------
DROP TABLE IF EXISTS `shops`;
CREATE TABLE `shops`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `store` varchar(100) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `item` varchar(100) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `price` int(11) NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 7 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of shops
-- ----------------------------
INSERT INTO `shops` VALUES (1, 'TwentyFourSeven', 'bread', 30);
INSERT INTO `shops` VALUES (2, 'TwentyFourSeven', 'water', 15);
INSERT INTO `shops` VALUES (3, 'RobsLiquor', 'bread', 30);
INSERT INTO `shops` VALUES (4, 'RobsLiquor', 'water', 15);
INSERT INTO `shops` VALUES (5, 'LTDgasoline', 'bread', 30);
INSERT INTO `shops` VALUES (6, 'LTDgasoline', 'water', 15);

-- ----------------------------
-- Table structure for society_moneywash
-- ----------------------------
DROP TABLE IF EXISTS `society_moneywash`;
CREATE TABLE `society_moneywash`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `identifier` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `society` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `amount` int(11) NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for user_accounts
-- ----------------------------
DROP TABLE IF EXISTS `user_accounts`;
CREATE TABLE `user_accounts`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `identifier` varchar(22) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `name` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `money` double NOT NULL DEFAULT 0,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for user_contacts
-- ----------------------------
DROP TABLE IF EXISTS `user_contacts`;
CREATE TABLE `user_contacts`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `identifier` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `name` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `number` int(11) NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for user_inventory
-- ----------------------------
DROP TABLE IF EXISTS `user_inventory`;
CREATE TABLE `user_inventory`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `identifier` varchar(22) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `item` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `count` int(11) NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for user_licenses
-- ----------------------------
DROP TABLE IF EXISTS `user_licenses`;
CREATE TABLE `user_licenses`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `type` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `owner` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for user_parkings
-- ----------------------------
DROP TABLE IF EXISTS `user_parkings`;
CREATE TABLE `user_parkings`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `identifier` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `garage` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `zone` int(11) NOT NULL,
  `vehicle` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 1 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for users
-- ----------------------------
DROP TABLE IF EXISTS `users`;
CREATE TABLE `users`  (
  `identifier` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `license` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `money` int(11) NULL DEFAULT NULL,
  `name` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT '',
  `skin` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL,
  `job` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT 'unemployed',
  `job_grade` int(11) NULL DEFAULT 0,
  `loadout` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL,
  `position` varchar(36) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `bank` int(11) NULL DEFAULT NULL,
  `permission_level` int(11) NULL DEFAULT NULL,
  `group` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `firstname` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT '',
  `lastname` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT '',
  `dateofbirth` varchar(25) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT '',
  `sex` varchar(10) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT '',
  `height` varchar(5) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT '',
  `phone_number` int(11) NULL DEFAULT NULL,
  `tattoos` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT '{}',
  `status` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL,
  `last_property` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  `is_dead` tinyint(1) NULL DEFAULT 0
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for vehicle_categories
-- ----------------------------
DROP TABLE IF EXISTS `vehicle_categories`;
CREATE TABLE `vehicle_categories`  (
  `name` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `label` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  PRIMARY KEY (`name`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of vehicle_categories
-- ----------------------------
INSERT INTO `vehicle_categories` VALUES ('compacts', 'Compacto');
INSERT INTO `vehicle_categories` VALUES ('coupes', 'Cupês');
INSERT INTO `vehicle_categories` VALUES ('motorcycles', 'Motos');
INSERT INTO `vehicle_categories` VALUES ('muscle', 'Muscle');
INSERT INTO `vehicle_categories` VALUES ('offroad', 'Off Road');
INSERT INTO `vehicle_categories` VALUES ('sedans', 'Sedans');
INSERT INTO `vehicle_categories` VALUES ('sports', 'Sports');
INSERT INTO `vehicle_categories` VALUES ('sportsclassics', 'Clássicos Esportivos');
INSERT INTO `vehicle_categories` VALUES ('super', 'Super');
INSERT INTO `vehicle_categories` VALUES ('suvs', 'SUVs');
INSERT INTO `vehicle_categories` VALUES ('vans', 'Vans');

-- ----------------------------
-- Table structure for vehicle_sold
-- ----------------------------
DROP TABLE IF EXISTS `vehicle_sold`;
CREATE TABLE `vehicle_sold`  (
  `client` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `model` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `plate` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `soldby` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `date` varchar(50) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  PRIMARY KEY (`plate`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Table structure for vehicles
-- ----------------------------
DROP TABLE IF EXISTS `vehicles`;
CREATE TABLE `vehicles`  (
  `name` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `model` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `price` int(11) NOT NULL,
  `category` varchar(60) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL DEFAULT NULL,
  PRIMARY KEY (`model`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of vehicles
-- ----------------------------
INSERT INTO `vehicles` VALUES ('Akuma', 'AKUMA', 7500, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Adder', 'adder', 900000, 'super');
INSERT INTO `vehicles` VALUES ('Alpha', 'alpha', 60000, 'sports');
INSERT INTO `vehicles` VALUES ('Ardent', 'ardent', 1150000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Asea', 'asea', 5500, 'sedans');
INSERT INTO `vehicles` VALUES ('Autarch', 'autarch', 1955000, 'super');
INSERT INTO `vehicles` VALUES ('Avarus', 'avarus', 18000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Bagger', 'bagger', 13500, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Baller', 'baller2', 40000, 'suvs');
INSERT INTO `vehicles` VALUES ('Baller Sport', 'baller3', 60000, 'suvs');
INSERT INTO `vehicles` VALUES ('Banshee', 'banshee', 70000, 'sports');
INSERT INTO `vehicles` VALUES ('Banshee 900R', 'banshee2', 255000, 'super');
INSERT INTO `vehicles` VALUES ('Bati 801', 'bati', 12000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Bati 801RR', 'bati2', 19000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Bestia GTS', 'bestiagts', 55000, 'sports');
INSERT INTO `vehicles` VALUES ('BF400', 'bf400', 6500, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Bf Injection', 'bfinjection', 16000, 'offroad');
INSERT INTO `vehicles` VALUES ('Bifta', 'bifta', 12000, 'offroad');
INSERT INTO `vehicles` VALUES ('Bison', 'bison', 45000, 'vans');
INSERT INTO `vehicles` VALUES ('Blade', 'blade', 15000, 'muscle');
INSERT INTO `vehicles` VALUES ('Blazer', 'blazer', 6500, 'offroad');
INSERT INTO `vehicles` VALUES ('Blazer Sport', 'blazer4', 8500, 'offroad');
INSERT INTO `vehicles` VALUES ('blazer5', 'blazer5', 1755600, 'offroad');
INSERT INTO `vehicles` VALUES ('Blista', 'blista', 8000, 'compacts');
INSERT INTO `vehicles` VALUES ('BMX (velo)', 'bmx', 160, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Bobcat XL', 'bobcatxl', 32000, 'vans');
INSERT INTO `vehicles` VALUES ('Brawler', 'brawler', 45000, 'offroad');
INSERT INTO `vehicles` VALUES ('Brioso R/A', 'brioso', 18000, 'compacts');
INSERT INTO `vehicles` VALUES ('Btype', 'btype', 62000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Btype Hotroad', 'btype2', 155000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Btype Luxe', 'btype3', 85000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Buccaneer', 'buccaneer', 18000, 'muscle');
INSERT INTO `vehicles` VALUES ('Buccaneer Rider', 'buccaneer2', 24000, 'muscle');
INSERT INTO `vehicles` VALUES ('Buffalo', 'buffalo', 12000, 'sports');
INSERT INTO `vehicles` VALUES ('Buffalo S', 'buffalo2', 20000, 'sports');
INSERT INTO `vehicles` VALUES ('Bullet', 'bullet', 90000, 'super');
INSERT INTO `vehicles` VALUES ('Burrito', 'burrito3', 19000, 'vans');
INSERT INTO `vehicles` VALUES ('Camper', 'camper', 42000, 'vans');
INSERT INTO `vehicles` VALUES ('Carbonizzare', 'carbonizzare', 75000, 'sports');
INSERT INTO `vehicles` VALUES ('Carbon RS', 'carbonrs', 18000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Casco', 'casco', 30000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Cavalcade', 'cavalcade2', 55000, 'suvs');
INSERT INTO `vehicles` VALUES ('Cheetah', 'cheetah', 375000, 'super');
INSERT INTO `vehicles` VALUES ('Chimera', 'chimera', 38000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Chino', 'chino', 15000, 'muscle');
INSERT INTO `vehicles` VALUES ('Chino Luxe', 'chino2', 19000, 'muscle');
INSERT INTO `vehicles` VALUES ('Cliffhanger', 'cliffhanger', 9500, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Cognoscenti Cabrio', 'cogcabrio', 55000, 'coupes');
INSERT INTO `vehicles` VALUES ('Cognoscenti', 'cognoscenti', 55000, 'sedans');
INSERT INTO `vehicles` VALUES ('Comet', 'comet2', 65000, 'sports');
INSERT INTO `vehicles` VALUES ('Comet 5', 'comet5', 1145000, 'sports');
INSERT INTO `vehicles` VALUES ('Contender', 'contender', 70000, 'suvs');
INSERT INTO `vehicles` VALUES ('Coquette', 'coquette', 65000, 'sports');
INSERT INTO `vehicles` VALUES ('Coquette Classic', 'coquette2', 40000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Coquette BlackFin', 'coquette3', 55000, 'muscle');
INSERT INTO `vehicles` VALUES ('Cruiser (velo)', 'cruiser', 510, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Cyclone', 'cyclone', 1890000, 'super');
INSERT INTO `vehicles` VALUES ('Daemon', 'daemon', 11500, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Daemon High', 'daemon2', 13500, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Defiler', 'defiler', 9800, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Deluxo', 'deluxo', 4721500, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Dominator', 'dominator', 35000, 'muscle');
INSERT INTO `vehicles` VALUES ('Double T', 'double', 28000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Dubsta', 'dubsta', 45000, 'suvs');
INSERT INTO `vehicles` VALUES ('Dubsta Luxuary', 'dubsta2', 60000, 'suvs');
INSERT INTO `vehicles` VALUES ('Bubsta 6x6', 'dubsta3', 120000, 'offroad');
INSERT INTO `vehicles` VALUES ('Dukes', 'dukes', 28000, 'muscle');
INSERT INTO `vehicles` VALUES ('Dune Buggy', 'dune', 8000, 'offroad');
INSERT INTO `vehicles` VALUES ('Elegy', 'elegy2', 38500, 'sports');
INSERT INTO `vehicles` VALUES ('Emperor', 'emperor', 8500, 'sedans');
INSERT INTO `vehicles` VALUES ('Enduro', 'enduro', 5500, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Entity XF', 'entityxf', 425000, 'super');
INSERT INTO `vehicles` VALUES ('Esskey', 'esskey', 4200, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Exemplar', 'exemplar', 32000, 'coupes');
INSERT INTO `vehicles` VALUES ('F620', 'f620', 40000, 'coupes');
INSERT INTO `vehicles` VALUES ('Faction', 'faction', 20000, 'muscle');
INSERT INTO `vehicles` VALUES ('Faction Rider', 'faction2', 30000, 'muscle');
INSERT INTO `vehicles` VALUES ('Faction XL', 'faction3', 40000, 'muscle');
INSERT INTO `vehicles` VALUES ('Faggio', 'faggio', 1900, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Vespa', 'faggio2', 2800, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Felon', 'felon', 42000, 'coupes');
INSERT INTO `vehicles` VALUES ('Felon GT', 'felon2', 55000, 'coupes');
INSERT INTO `vehicles` VALUES ('Feltzer', 'feltzer2', 55000, 'sports');
INSERT INTO `vehicles` VALUES ('Stirling GT', 'feltzer3', 65000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Fixter (velo)', 'fixter', 225, 'motorcycles');
INSERT INTO `vehicles` VALUES ('FMJ', 'fmj', 185000, 'super');
INSERT INTO `vehicles` VALUES ('Fhantom', 'fq2', 17000, 'suvs');
INSERT INTO `vehicles` VALUES ('Fugitive', 'fugitive', 12000, 'sedans');
INSERT INTO `vehicles` VALUES ('Furore GT', 'furoregt', 45000, 'sports');
INSERT INTO `vehicles` VALUES ('Fusilade', 'fusilade', 40000, 'sports');
INSERT INTO `vehicles` VALUES ('Gargoyle', 'gargoyle', 16500, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Gauntlet', 'gauntlet', 30000, 'muscle');
INSERT INTO `vehicles` VALUES ('Gang Burrito', 'gburrito', 45000, 'vans');
INSERT INTO `vehicles` VALUES ('Burrito', 'gburrito2', 29000, 'vans');
INSERT INTO `vehicles` VALUES ('Glendale', 'glendale', 6500, 'sedans');
INSERT INTO `vehicles` VALUES ('Grabger', 'granger', 50000, 'suvs');
INSERT INTO `vehicles` VALUES ('Gresley', 'gresley', 47500, 'suvs');
INSERT INTO `vehicles` VALUES ('GT 500', 'gt500', 785000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Guardian', 'guardian', 45000, 'offroad');
INSERT INTO `vehicles` VALUES ('Hakuchou', 'hakuchou', 31000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Hakuchou Sport', 'hakuchou2', 55000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Hermes', 'hermes', 535000, 'muscle');
INSERT INTO `vehicles` VALUES ('Hexer', 'hexer', 12000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Hotknife', 'hotknife', 125000, 'muscle');
INSERT INTO `vehicles` VALUES ('Huntley S', 'huntley', 40000, 'suvs');
INSERT INTO `vehicles` VALUES ('Hustler', 'hustler', 625000, 'muscle');
INSERT INTO `vehicles` VALUES ('Infernus', 'infernus', 180000, 'super');
INSERT INTO `vehicles` VALUES ('Innovation', 'innovation', 23500, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Intruder', 'intruder', 7500, 'sedans');
INSERT INTO `vehicles` VALUES ('Issi', 'issi2', 10000, 'compacts');
INSERT INTO `vehicles` VALUES ('Jackal', 'jackal', 38000, 'coupes');
INSERT INTO `vehicles` VALUES ('Jester', 'jester', 65000, 'sports');
INSERT INTO `vehicles` VALUES ('Jester(Racecar)', 'jester2', 135000, 'sports');
INSERT INTO `vehicles` VALUES ('Journey', 'journey', 6500, 'vans');
INSERT INTO `vehicles` VALUES ('Kamacho', 'kamacho', 345000, 'offroad');
INSERT INTO `vehicles` VALUES ('Khamelion', 'khamelion', 38000, 'sports');
INSERT INTO `vehicles` VALUES ('Kuruma', 'kuruma', 30000, 'sports');
INSERT INTO `vehicles` VALUES ('Landstalker', 'landstalker', 35000, 'suvs');
INSERT INTO `vehicles` VALUES ('RE-7B', 'le7b', 325000, 'super');
INSERT INTO `vehicles` VALUES ('Lynx', 'lynx', 40000, 'sports');
INSERT INTO `vehicles` VALUES ('Mamba', 'mamba', 70000, 'sports');
INSERT INTO `vehicles` VALUES ('Manana', 'manana', 12800, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Manchez', 'manchez', 5300, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Massacro', 'massacro', 65000, 'sports');
INSERT INTO `vehicles` VALUES ('Massacro(Racecar)', 'massacro2', 130000, 'sports');
INSERT INTO `vehicles` VALUES ('Mesa', 'mesa', 16000, 'suvs');
INSERT INTO `vehicles` VALUES ('Mesa Trail', 'mesa3', 40000, 'suvs');
INSERT INTO `vehicles` VALUES ('Minivan', 'minivan', 13000, 'vans');
INSERT INTO `vehicles` VALUES ('Monroe', 'monroe', 55000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('The Liberator', 'monster', 210000, 'offroad');
INSERT INTO `vehicles` VALUES ('Moonbeam', 'moonbeam', 18000, 'vans');
INSERT INTO `vehicles` VALUES ('Moonbeam Rider', 'moonbeam2', 35000, 'vans');
INSERT INTO `vehicles` VALUES ('Nemesis', 'nemesis', 5800, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Neon', 'neon', 1500000, 'sports');
INSERT INTO `vehicles` VALUES ('Nightblade', 'nightblade', 35000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Nightshade', 'nightshade', 65000, 'muscle');
INSERT INTO `vehicles` VALUES ('9F', 'ninef', 65000, 'sports');
INSERT INTO `vehicles` VALUES ('9F Cabrio', 'ninef2', 80000, 'sports');
INSERT INTO `vehicles` VALUES ('Omnis', 'omnis', 35000, 'sports');
INSERT INTO `vehicles` VALUES ('Oppressor', 'oppressor', 3524500, 'super');
INSERT INTO `vehicles` VALUES ('Oracle XS', 'oracle2', 35000, 'coupes');
INSERT INTO `vehicles` VALUES ('Osiris', 'osiris', 160000, 'super');
INSERT INTO `vehicles` VALUES ('Panto', 'panto', 10000, 'compacts');
INSERT INTO `vehicles` VALUES ('Paradise', 'paradise', 19000, 'vans');
INSERT INTO `vehicles` VALUES ('Pariah', 'pariah', 1420000, 'sports');
INSERT INTO `vehicles` VALUES ('Patriot', 'patriot', 55000, 'suvs');
INSERT INTO `vehicles` VALUES ('PCJ-600', 'pcj', 6200, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Penumbra', 'penumbra', 28000, 'sports');
INSERT INTO `vehicles` VALUES ('Pfister', 'pfister811', 85000, 'super');
INSERT INTO `vehicles` VALUES ('Phoenix', 'phoenix', 12500, 'muscle');
INSERT INTO `vehicles` VALUES ('Picador', 'picador', 18000, 'muscle');
INSERT INTO `vehicles` VALUES ('Pigalle', 'pigalle', 20000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Prairie', 'prairie', 12000, 'compacts');
INSERT INTO `vehicles` VALUES ('Premier', 'premier', 8000, 'sedans');
INSERT INTO `vehicles` VALUES ('Primo Custom', 'primo2', 14000, 'sedans');
INSERT INTO `vehicles` VALUES ('X80 Proto', 'prototipo', 2500000, 'super');
INSERT INTO `vehicles` VALUES ('Radius', 'radi', 29000, 'suvs');
INSERT INTO `vehicles` VALUES ('raiden', 'raiden', 1375000, 'sports');
INSERT INTO `vehicles` VALUES ('Rapid GT', 'rapidgt', 35000, 'sports');
INSERT INTO `vehicles` VALUES ('Rapid GT Convertible', 'rapidgt2', 45000, 'sports');
INSERT INTO `vehicles` VALUES ('Rapid GT3', 'rapidgt3', 885000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Reaper', 'reaper', 150000, 'super');
INSERT INTO `vehicles` VALUES ('Rebel', 'rebel2', 35000, 'offroad');
INSERT INTO `vehicles` VALUES ('Regina', 'regina', 5000, 'sedans');
INSERT INTO `vehicles` VALUES ('Retinue', 'retinue', 615000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Revolter', 'revolter', 1610000, 'sports');
INSERT INTO `vehicles` VALUES ('riata', 'riata', 380000, 'offroad');
INSERT INTO `vehicles` VALUES ('Rocoto', 'rocoto', 45000, 'suvs');
INSERT INTO `vehicles` VALUES ('Ruffian', 'ruffian', 6800, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Ruiner 2', 'ruiner2', 5745600, 'muscle');
INSERT INTO `vehicles` VALUES ('Rumpo', 'rumpo', 15000, 'vans');
INSERT INTO `vehicles` VALUES ('Rumpo Trail', 'rumpo3', 19500, 'vans');
INSERT INTO `vehicles` VALUES ('Sabre Turbo', 'sabregt', 20000, 'muscle');
INSERT INTO `vehicles` VALUES ('Sabre GT', 'sabregt2', 25000, 'muscle');
INSERT INTO `vehicles` VALUES ('Sanchez', 'sanchez', 5300, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Sanchez Sport', 'sanchez2', 5300, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Sanctus', 'sanctus', 25000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Sandking', 'sandking', 55000, 'offroad');
INSERT INTO `vehicles` VALUES ('Savestra', 'savestra', 990000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('SC 1', 'sc1', 1603000, 'super');
INSERT INTO `vehicles` VALUES ('Schafter', 'schafter2', 25000, 'sedans');
INSERT INTO `vehicles` VALUES ('Schafter V12', 'schafter3', 50000, 'sports');
INSERT INTO `vehicles` VALUES ('Scorcher (velo)', 'scorcher', 280, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Seminole', 'seminole', 25000, 'suvs');
INSERT INTO `vehicles` VALUES ('Sentinel', 'sentinel', 32000, 'coupes');
INSERT INTO `vehicles` VALUES ('Sentinel XS', 'sentinel2', 40000, 'coupes');
INSERT INTO `vehicles` VALUES ('Sentinel3', 'sentinel3', 650000, 'sports');
INSERT INTO `vehicles` VALUES ('Seven 70', 'seven70', 39500, 'sports');
INSERT INTO `vehicles` VALUES ('ETR1', 'sheava', 220000, 'super');
INSERT INTO `vehicles` VALUES ('Shotaro Concept', 'shotaro', 320000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Slam Van', 'slamvan3', 11500, 'muscle');
INSERT INTO `vehicles` VALUES ('Sovereign', 'sovereign', 22000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Stinger', 'stinger', 80000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Stinger GT', 'stingergt', 75000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Streiter', 'streiter', 500000, 'sports');
INSERT INTO `vehicles` VALUES ('Stretch', 'stretch', 90000, 'sedans');
INSERT INTO `vehicles` VALUES ('Stromberg', 'stromberg', 3185350, 'sports');
INSERT INTO `vehicles` VALUES ('Sultan', 'sultan', 15000, 'sports');
INSERT INTO `vehicles` VALUES ('Sultan RS', 'sultanrs', 65000, 'super');
INSERT INTO `vehicles` VALUES ('Super Diamond', 'superd', 130000, 'sedans');
INSERT INTO `vehicles` VALUES ('Surano', 'surano', 50000, 'sports');
INSERT INTO `vehicles` VALUES ('Surfer', 'surfer', 12000, 'vans');
INSERT INTO `vehicles` VALUES ('T20', 't20', 300000, 'super');
INSERT INTO `vehicles` VALUES ('Tailgater', 'tailgater', 30000, 'sedans');
INSERT INTO `vehicles` VALUES ('Tampa', 'tampa', 16000, 'muscle');
INSERT INTO `vehicles` VALUES ('Drift Tampa', 'tampa2', 80000, 'sports');
INSERT INTO `vehicles` VALUES ('Thrust', 'thrust', 24000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Tri bike (velo)', 'tribike3', 520, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Trophy Truck', 'trophytruck', 60000, 'offroad');
INSERT INTO `vehicles` VALUES ('Trophy Truck Limited', 'trophytruck2', 80000, 'offroad');
INSERT INTO `vehicles` VALUES ('Tropos', 'tropos', 40000, 'sports');
INSERT INTO `vehicles` VALUES ('Turismo R', 'turismor', 350000, 'super');
INSERT INTO `vehicles` VALUES ('Tyrus', 'tyrus', 600000, 'super');
INSERT INTO `vehicles` VALUES ('Vacca', 'vacca', 120000, 'super');
INSERT INTO `vehicles` VALUES ('Vader', 'vader', 7200, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Verlierer', 'verlierer2', 70000, 'sports');
INSERT INTO `vehicles` VALUES ('Vigero', 'vigero', 12500, 'muscle');
INSERT INTO `vehicles` VALUES ('Virgo', 'virgo', 14000, 'muscle');
INSERT INTO `vehicles` VALUES ('Viseris', 'viseris', 875000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Visione', 'visione', 2250000, 'super');
INSERT INTO `vehicles` VALUES ('Voltic', 'voltic', 90000, 'super');
INSERT INTO `vehicles` VALUES ('Voltic 2', 'voltic2', 3830400, 'super');
INSERT INTO `vehicles` VALUES ('Voodoo', 'voodoo', 7200, 'muscle');
INSERT INTO `vehicles` VALUES ('Vortex', 'vortex', 9800, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Warrener', 'warrener', 4000, 'sedans');
INSERT INTO `vehicles` VALUES ('Washington', 'washington', 9000, 'sedans');
INSERT INTO `vehicles` VALUES ('Windsor', 'windsor', 95000, 'coupes');
INSERT INTO `vehicles` VALUES ('Windsor Drop', 'windsor2', 125000, 'coupes');
INSERT INTO `vehicles` VALUES ('Woflsbane', 'wolfsbane', 9000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('XLS', 'xls', 32000, 'suvs');
INSERT INTO `vehicles` VALUES ('Yosemite', 'yosemite', 485000, 'muscle');
INSERT INTO `vehicles` VALUES ('Youga', 'youga', 10800, 'vans');
INSERT INTO `vehicles` VALUES ('Youga Luxuary', 'youga2', 14500, 'vans');
INSERT INTO `vehicles` VALUES ('Z190', 'z190', 900000, 'sportsclassics');
INSERT INTO `vehicles` VALUES ('Zentorno', 'zentorno', 1500000, 'super');
INSERT INTO `vehicles` VALUES ('Zion', 'zion', 36000, 'coupes');
INSERT INTO `vehicles` VALUES ('Zion Cabrio', 'zion2', 45000, 'coupes');
INSERT INTO `vehicles` VALUES ('Zombie', 'zombiea', 9500, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Zombie Luxuary', 'zombieb', 12000, 'motorcycles');
INSERT INTO `vehicles` VALUES ('Z-Type', 'ztype', 220000, 'sportsclassics');

-- ----------------------------
-- Table structure for weashops
-- ----------------------------
DROP TABLE IF EXISTS `weashops`;
CREATE TABLE `weashops`  (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `zone` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `item` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `price` int(11) NOT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 41 CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

-- ----------------------------
-- Records of weashops
-- ----------------------------
INSERT INTO `weashops` VALUES (1, 'GunShop', 'WEAPON_PISTOL', 300);
INSERT INTO `weashops` VALUES (2, 'BlackWeashop', 'WEAPON_PISTOL', 500);
INSERT INTO `weashops` VALUES (3, 'GunShop', 'WEAPON_FLASHLIGHT', 60);
INSERT INTO `weashops` VALUES (4, 'BlackWeashop', 'WEAPON_FLASHLIGHT', 70);
INSERT INTO `weashops` VALUES (5, 'GunShop', 'WEAPON_MACHETE', 90);
INSERT INTO `weashops` VALUES (6, 'BlackWeashop', 'WEAPON_MACHETE', 110);
INSERT INTO `weashops` VALUES (7, 'GunShop', 'WEAPON_NIGHTSTICK', 150);
INSERT INTO `weashops` VALUES (8, 'BlackWeashop', 'WEAPON_NIGHTSTICK', 150);
INSERT INTO `weashops` VALUES (9, 'GunShop', 'WEAPON_BAT', 100);
INSERT INTO `weashops` VALUES (10, 'BlackWeashop', 'WEAPON_BAT', 100);
INSERT INTO `weashops` VALUES (11, 'GunShop', 'WEAPON_STUNGUN', 50);
INSERT INTO `weashops` VALUES (12, 'BlackWeashop', 'WEAPON_STUNGUN', 50);
INSERT INTO `weashops` VALUES (13, 'GunShop', 'WEAPON_MICROSMG', 1400);
INSERT INTO `weashops` VALUES (14, 'BlackWeashop', 'WEAPON_MICROSMG', 1700);
INSERT INTO `weashops` VALUES (15, 'GunShop', 'WEAPON_PUMPSHOTGUN', 3400);
INSERT INTO `weashops` VALUES (16, 'BlackWeashop', 'WEAPON_PUMPSHOTGUN', 3500);
INSERT INTO `weashops` VALUES (17, 'GunShop', 'WEAPON_ASSAULTRIFLE', 10000);
INSERT INTO `weashops` VALUES (18, 'BlackWeashop', 'WEAPON_ASSAULTRIFLE', 11000);
INSERT INTO `weashops` VALUES (19, 'GunShop', 'WEAPON_SPECIALCARBINE', 15000);
INSERT INTO `weashops` VALUES (20, 'BlackWeashop', 'WEAPON_SPECIALCARBINE', 16500);
INSERT INTO `weashops` VALUES (21, 'GunShop', 'WEAPON_SNIPERRIFLE', 22000);
INSERT INTO `weashops` VALUES (22, 'BlackWeashop', 'WEAPON_SNIPERRIFLE', 24000);
INSERT INTO `weashops` VALUES (23, 'GunShop', 'WEAPON_FIREWORK', 18000);
INSERT INTO `weashops` VALUES (24, 'BlackWeashop', 'WEAPON_FIREWORK', 20000);
INSERT INTO `weashops` VALUES (25, 'GunShop', 'WEAPON_GRENADE', 500);
INSERT INTO `weashops` VALUES (26, 'BlackWeashop', 'WEAPON_GRENADE', 650);
INSERT INTO `weashops` VALUES (27, 'GunShop', 'WEAPON_BZGAS', 200);
INSERT INTO `weashops` VALUES (28, 'BlackWeashop', 'WEAPON_BZGAS', 350);
INSERT INTO `weashops` VALUES (29, 'GunShop', 'WEAPON_FIREEXTINGUISHER', 100);
INSERT INTO `weashops` VALUES (30, 'BlackWeashop', 'WEAPON_FIREEXTINGUISHER', 100);
INSERT INTO `weashops` VALUES (31, 'GunShop', 'WEAPON_BALL', 50);
INSERT INTO `weashops` VALUES (32, 'BlackWeashop', 'WEAPON_BALL', 50);
INSERT INTO `weashops` VALUES (33, 'GunShop', 'WEAPON_SMOKEGRENADE', 100);
INSERT INTO `weashops` VALUES (34, 'BlackWeashop', 'WEAPON_SMOKEGRENADE', 100);
INSERT INTO `weashops` VALUES (35, 'BlackWeashop', 'WEAPON_APPISTOL', 1100);
INSERT INTO `weashops` VALUES (36, 'BlackWeashop', 'WEAPON_CARBINERIFLE', 12000);
INSERT INTO `weashops` VALUES (37, 'BlackWeashop', 'WEAPON_HEAVYSNIPER', 30000);
INSERT INTO `weashops` VALUES (38, 'BlackWeashop', 'WEAPON_MINIGUN', 45000);
INSERT INTO `weashops` VALUES (39, 'BlackWeashop', 'WEAPON_RAILGUN', 50000);
INSERT INTO `weashops` VALUES (40, 'BlackWeashop', 'WEAPON_STICKYBOMB', 500);

-- ----------------------------
-- Table structure for whitelist
-- ----------------------------
DROP TABLE IF EXISTS `whitelist`;
CREATE TABLE `whitelist`  (
  `identifier` varchar(70) CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL,
  `last_connection` timestamp(0) NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP(0),
  `ban_reason` text CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NULL,
  `ban_until` timestamp(0) NULL DEFAULT NULL,
  `vip` int(11) NOT NULL DEFAULT 0,
  PRIMARY KEY (`identifier`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_bin ROW_FORMAT = Compact;

SET FOREIGN_KEY_CHECKS = 1;
```

## **EXEMPLO DE INICIALIZADOR.BAT**

```text
@CHCP 1252 >NUL
@echo off
@title FiveM Server - ESX Brasil
cls
color 02
:start
echo.
echo.
echo.
echo =============================
echo ######### ######### ###   ###
echo ##        ##          ## ##
echo ######### #########    ###
echo ##               ##   ## ##
echo ######### ######### ###   ###
echo =============================
echo.
echo.
echo.
echo =========================================
echo #####  #####  ####### ####### ## ##
echo ##  ## ##  ## ##   ## ##      ## ##
echo #####  ####   ####### ####### ## ##
echo ##  ## ## ##  ##   ##      ## ## ##
echo #####  ## ##  ##   ## ####### ## ########
echo =========================================
echo.
echo.
echo.
echo  Aguarde...
echo.
echo.

timeout /t 3 >null

:choice
set /P  c=Deseja excluir o cache? (S/N)
if /I "%c%" EQU "S" goto :somewhere
if /I "%c%" EQU "N" goto :somewhere_else
goto :choice
:somewhere
echo.
echo.
echo  Excluindo...
 rd /s /q "C:\TESTE\cache"

timeout /t 3 >null

echo %time% - O cache foi excluído.

timeout /t 3 >null

:somewhere_else
start C:\TESTE\start.bat
echo %time% - O servidor está iniciando...

timeout /t 2 >null
echo %time% - Inicializando resources...

timeout /t 3 >null
echo %time% - O servidor está online.
```

**Muda para sua pasta**

Na linha **45** e na **54** mude para sua pasta de seu servidor!   
****Mude somente o nome “**TESTE**” para sua pasta!

## **EXEMPLO START.BAT**

```text
start "Server" C:\TESTE\run.cmd +exec server.cfg
```

**Muda para sua pasta**

Na linha **1** mude para sua pasta de seu servidor!   
Mude somente o nome “**TESTE**” para sua pasta!

