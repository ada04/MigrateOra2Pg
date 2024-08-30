# PIVOT, UNPIVOT and MERGE in Oracle 21c and analogs in PostgreSQL

## Load example data fot PIVOT

### Load example data in Oracle

```sql
alter pluggable database pdb1 open;
alter pluggable database pdb1 save state;

create user scott identified by tiger;
grant connect, resource to scott;
alter user scott quota unlimited on users;

create table scott.clients (client_id number(2) not null, firstname varchar2(100) not null, lastname varchar2(100) not null, PRIMARY KEY (client_id));
create table scott.services (service_id number(2) not null, servname varchar2(100) not null, PRIMARY KEY (service_id));
create table scott.payments (pmnt_id number(4) not null, client_id number(2) not null, service_id number(2) not null, period number(6) not null, amount number(10) not null, data date default sysdate, PRIMARY KEY (pmnt_id));
create table scott.charges (chg_id number(4) not null, client_id number(2) not null, service_id number(2) not null, period number(6) not null, amount number(10) not null, data date default sysdate, PRIMARY KEY (chg_id));

alter table scott.payments add constraint pmnt_cl_fk foreign key(client_id) references scott.clients(client_id);
alter table scott.payments add constraint pmnt_srv_fk foreign key(service_id) references scott.services(service_id);
alter table scott.charges add constraint chg_cl_fk foreign key(client_id) references scott.clients(client_id);
alter table scott.charges add constraint vhg_srv_fk foreign key(service_id) references scott.services(service_id);

create index scott.charges_clid on scott.charges(client_id);
create index scott.charges_servid on scott.charges(service_id);
create index scott.charges_period on scott.charges(period);

create index scott.payments_clid on scott.payments(client_id);
create index scott.payments_servid on scott.payments(service_id);
create index scott.payments_period on scott.payments(period);

insert into scott.clients(client_id, firstname, lastname) values (1, 'Кирилл', 'Иванов');
insert into scott.clients(client_id, firstname, lastname) values (2, 'Павел', 'Ветров');
insert into scott.clients(client_id, firstname, lastname) values (3, 'Иван', 'Сидоров');
insert into scott.clients(client_id, firstname, lastname) values (4, 'Артём', 'Солнцев');
insert into scott.clients(client_id, firstname, lastname) values (5, 'Ирина', 'Авдеева');

insert into scott.services(service_id, servname) values (1, 'Электроэнергия');
insert into scott.services(service_id, servname) values (2, 'Газоснабжение');
insert into scott.services(service_id, servname) values (3, 'ХВС');
insert into scott.services(service_id, servname) values (4, 'ГВС');

insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(1,1,1,202401,393688);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(2,1,2,202401,535262);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(3,1,3,202401,252111);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(4,1,4,202401,549400);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(5,2,1,202401,291387);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(6,2,2,202401,121710);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(7,2,3,202401,251687);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(8,2,4,202401,234442);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(9,3,1,202401,127024);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(10,3,2,202401,98551);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(11,3,3,202401,142665);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(12,3,4,202401,38300);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(13,4,1,202401,194238);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(14,4,2,202401,25908);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(15,4,3,202401,51409);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(16,4,4,202401,211553);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(17,5,1,202401,558190);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(18,5,2,202401,73086);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(19,5,3,202401,113265);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(20,5,4,202401,119883);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(21,1,1,202402,179165);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(22,1,2,202402,215382);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(23,1,3,202402,71226);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(24,1,4,202402,52900);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(25,2,1,202402,393210);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(26,2,2,202402,156507);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(27,2,3,202402,157640);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(28,2,4,202402,63298);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(29,3,1,202402,40398);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(30,3,2,202402,17956);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(31,3,3,202402,231604);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(32,3,4,202402,462956);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(33,4,1,202402,232677);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(34,4,2,202402,143458);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(35,4,3,202402,254717);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(36,4,4,202402,236280);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(37,5,1,202402,47384);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(38,5,2,202402,187564);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(39,5,3,202402,199996);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(40,5,4,202402,191467);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(41,1,1,202403,153511);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(42,1,2,202403,563614);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(43,1,3,202403,154496);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(44,1,4,202403,80226);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(45,2,1,202403,24180);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(46,2,2,202403,343730);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(47,2,3,202403,275515);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(48,2,4,202403,41773);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(49,3,1,202403,45739);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(50,3,2,202403,17296);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(51,3,3,202403,68541);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(52,3,4,202403,384434);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(53,4,1,202403,123170);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(54,4,2,202403,12325);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(55,4,3,202403,259238);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(56,4,4,202403,102227);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(57,5,1,202403,39963);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(58,5,2,202403,134616);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(59,5,3,202403,244556);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(60,5,4,202403,207876);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(61,1,1,202404,481696);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(62,1,2,202404,64905);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(63,1,3,202404,261908);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(64,1,4,202404,232780);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(65,2,1,202404,26320);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(66,2,2,202404,100256);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(67,2,3,202404,275532);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(68,2,4,202404,57968);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(69,3,1,202404,137822);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(70,3,2,202404,100753);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(71,3,3,202404,156903);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(72,3,4,202404,176722);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(73,4,1,202404,28983);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(74,4,2,202404,34494);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(75,4,3,202404,400334);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(76,4,4,202404,199721);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(77,5,1,202404,43758);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(78,5,2,202404,235874);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(79,5,3,202404,224269);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(80,5,4,202404,63588);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(81,1,1,202405,25199);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(82,1,2,202405,34538);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(83,1,3,202405,343718);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(84,1,4,202405,176656);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(85,2,1,202405,264023);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(86,2,2,202405,268814);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(87,2,3,202405,275766);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(88,2,4,202405,104226);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(89,3,1,202405,127990);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(90,3,2,202405,116280);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(91,3,3,202405,165533);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(92,3,4,202405,18549);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(93,4,1,202405,320624);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(94,4,2,202405,114944);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(95,4,3,202405,100454);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(96,4,4,202405,288648);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(97,5,1,202405,25805);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(98,5,2,202405,60557);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(99,5,3,202405,91417);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(100,5,4,202405,252524);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(101,1,1,202406,66839);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(102,1,2,202406,63863);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(103,1,3,202406,30736);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(104,1,4,202406,24300);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(105,2,1,202406,135711);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(106,2,2,202406,572334);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(107,2,3,202406,35079);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(108,2,4,202406,136708);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(109,3,1,202406,254618);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(110,3,2,202406,31144);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(111,3,3,202406,125499);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(112,3,4,202406,223842);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(113,4,1,202406,44533);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(114,4,2,202406,68948);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(115,4,3,202406,179067);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(116,4,4,202406,130514);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(117,5,1,202406,92616);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(118,5,2,202406,182021);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(119,5,3,202406,64297);
insert into scott.payments (pmnt_id, client_id, service_id, period, amount) values(120,5,4,202406,424842);

insert into scott.charges (chg_id, client_id, service_id, period, amount) values(1,1,1,202401,196844);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(2,1,2,202401,267631);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(3,1,3,202401,252111);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(4,1,4,202401,274700);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(5,2,1,202401,291387);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(6,2,2,202401,60855);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(7,2,3,202401,251687);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(8,2,4,202401,234442);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(9,3,1,202401,254048);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(10,3,2,202401,98551);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(11,3,3,202401,285330);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(12,3,4,202401,76600);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(13,4,1,202401,194238);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(14,4,2,202401,51815);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(15,4,3,202401,102817);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(16,4,4,202401,211553);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(17,5,1,202401,279095);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(18,5,2,202401,146172);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(19,5,3,202401,226530);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(20,5,4,202401,119883);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(21,1,1,202402,179165);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(22,1,2,202402,215382);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(23,1,3,202402,142452);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(24,1,4,202402,105799);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(25,2,1,202402,196605);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(26,2,2,202402,156507);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(27,2,3,202402,157640);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(28,2,4,202402,63298);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(29,3,1,202402,80795);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(30,3,2,202402,17956);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(31,3,3,202402,115802);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(32,3,4,202402,231478);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(33,4,1,202402,232677);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(34,4,2,202402,286915);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(35,4,3,202402,254717);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(36,4,4,202402,118140);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(37,5,1,202402,47384);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(38,5,2,202402,187564);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(39,5,3,202402,99998);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(40,5,4,202402,191467);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(41,1,1,202403,153511);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(42,1,2,202403,281807);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(43,1,3,202403,154496);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(44,1,4,202403,160451);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(45,2,1,202403,48359);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(46,2,2,202403,171865);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(47,2,3,202403,275515);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(48,2,4,202403,41773);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(49,3,1,202403,45739);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(50,3,2,202403,34592);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(51,3,3,202403,68541);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(52,3,4,202403,192217);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(53,4,1,202403,61585);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(54,4,2,202403,12325);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(55,4,3,202403,129619);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(56,4,4,202403,204454);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(57,5,1,202403,79926);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(58,5,2,202403,269231);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(59,5,3,202403,244556);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(60,5,4,202403,103938);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(61,1,1,202404,240848);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(62,1,2,202404,129809);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(63,1,3,202404,130954);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(64,1,4,202404,232780);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(65,2,1,202404,52639);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(66,2,2,202404,200512);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(67,2,3,202404,137766);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(68,2,4,202404,115935);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(69,3,1,202404,275643);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(70,3,2,202404,201506);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(71,3,3,202404,156903);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(72,3,4,202404,176722);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(73,4,1,202404,28983);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(74,4,2,202404,34494);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(75,4,3,202404,200167);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(76,4,4,202404,199721);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(77,5,1,202404,21879);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(78,5,2,202404,235874);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(79,5,3,202404,224269);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(80,5,4,202404,31794);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(81,1,1,202405,25199);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(82,1,2,202405,69075);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(83,1,3,202405,171859);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(84,1,4,202405,176656);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(85,2,1,202405,264023);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(86,2,2,202405,268814);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(87,2,3,202405,137883);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(88,2,4,202405,104226);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(89,3,1,202405,127990);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(90,3,2,202405,116280);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(91,3,3,202405,165533);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(92,3,4,202405,18549);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(93,4,1,202405,160312);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(94,4,2,202405,229888);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(95,4,3,202405,100454);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(96,4,4,202405,144324);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(97,5,1,202405,25805);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(98,5,2,202405,60557);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(99,5,3,202405,182833);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(100,5,4,202405,252524);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(101,1,1,202406,133678);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(102,1,2,202406,127726);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(103,1,3,202406,30736);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(104,1,4,202406,48600);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(105,2,1,202406,271421);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(106,2,2,202406,286167);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(107,2,3,202406,35079);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(108,2,4,202406,273416);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(109,3,1,202406,254618);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(110,3,2,202406,31144);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(111,3,3,202406,125499);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(112,3,4,202406,223842);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(113,4,1,202406,89065);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(114,4,2,202406,68948);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(115,4,3,202406,179067);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(116,4,4,202406,130514);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(117,5,1,202406,185231);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(118,5,2,202406,182021);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(119,5,3,202406,64297);
insert into scott.charges (chg_id, client_id, service_id, period, amount) values(120,5,4,202406,212421);

commit;
```

### Load example data in PostgreSQL

```sql
create table clients (client_id int2 not null, firstname varchar(100) not null, lastname varchar(100) not null, PRIMARY KEY (client_id));
create table services (service_id int2 not null, servname varchar(100) not null, PRIMARY KEY (service_id));
create table payments (pmnt_id int4 not null, client_id int2 not null, service_id int2 not null, period int4 not null, amount int4 not null, data date default now(), PRIMARY KEY (pmnt_id));
create table charges (chg_id int4 not null, client_id int2 not null, service_id int2 not null, period int4 not null, amount int4 not null, data date default now(), PRIMARY KEY (chg_id));

alter table payments add constraint pmnt_cl_fk foreign key(client_id) references clients(client_id);
alter table payments add constraint pmnt_srv_fk foreign key(service_id) references services(service_id);
alter table charges add constraint chg_cl_fk foreign key(client_id) references clients(client_id);
alter table charges add constraint vhg_srv_fk foreign key(service_id) references services(service_id);

create index charges_clid on charges(client_id);
create index charges_servid on charges(service_id);
create index charges_period on charges(period);

create index payments_clid on payments(client_id);
create index payments_servid on payments(service_id);
create index payments_period on payments(period);

insert into clients(client_id, firstname, lastname) values (1, 'Кирилл', 'Иванов');
insert into clients(client_id, firstname, lastname) values (2, 'Павел', 'Ветров');
insert into clients(client_id, firstname, lastname) values (3, 'Иван', 'Сидоров');
insert into clients(client_id, firstname, lastname) values (4, 'Артём', 'Солнцев');
insert into clients(client_id, firstname, lastname) values (5, 'Ирина', 'Авдеева');

insert into services(service_id, servname) values (1, 'Электроэнергия');
insert into services(service_id, servname) values (2, 'Газоснабжение');
insert into services(service_id, servname) values (3, 'ХВС');
insert into services(service_id, servname) values (4, 'ГВС');

insert into payments (pmnt_id, client_id, service_id, period, amount) values(1,1,1,202401,393688);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(2,1,2,202401,535262);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(3,1,3,202401,252111);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(4,1,4,202401,549400);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(5,2,1,202401,291387);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(6,2,2,202401,121710);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(7,2,3,202401,251687);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(8,2,4,202401,234442);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(9,3,1,202401,127024);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(10,3,2,202401,98551);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(11,3,3,202401,142665);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(12,3,4,202401,38300);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(13,4,1,202401,194238);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(14,4,2,202401,25908);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(15,4,3,202401,51409);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(16,4,4,202401,211553);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(17,5,1,202401,558190);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(18,5,2,202401,73086);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(19,5,3,202401,113265);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(20,5,4,202401,119883);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(21,1,1,202402,179165);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(22,1,2,202402,215382);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(23,1,3,202402,71226);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(24,1,4,202402,52900);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(25,2,1,202402,393210);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(26,2,2,202402,156507);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(27,2,3,202402,157640);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(28,2,4,202402,63298);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(29,3,1,202402,40398);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(30,3,2,202402,17956);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(31,3,3,202402,231604);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(32,3,4,202402,462956);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(33,4,1,202402,232677);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(34,4,2,202402,143458);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(35,4,3,202402,254717);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(36,4,4,202402,236280);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(37,5,1,202402,47384);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(38,5,2,202402,187564);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(39,5,3,202402,199996);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(40,5,4,202402,191467);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(41,1,1,202403,153511);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(42,1,2,202403,563614);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(43,1,3,202403,154496);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(44,1,4,202403,80226);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(45,2,1,202403,24180);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(46,2,2,202403,343730);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(47,2,3,202403,275515);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(48,2,4,202403,41773);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(49,3,1,202403,45739);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(50,3,2,202403,17296);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(51,3,3,202403,68541);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(52,3,4,202403,384434);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(53,4,1,202403,123170);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(54,4,2,202403,12325);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(55,4,3,202403,259238);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(56,4,4,202403,102227);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(57,5,1,202403,39963);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(58,5,2,202403,134616);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(59,5,3,202403,244556);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(60,5,4,202403,207876);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(61,1,1,202404,481696);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(62,1,2,202404,64905);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(63,1,3,202404,261908);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(64,1,4,202404,232780);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(65,2,1,202404,26320);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(66,2,2,202404,100256);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(67,2,3,202404,275532);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(68,2,4,202404,57968);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(69,3,1,202404,137822);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(70,3,2,202404,100753);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(71,3,3,202404,156903);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(72,3,4,202404,176722);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(73,4,1,202404,28983);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(74,4,2,202404,34494);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(75,4,3,202404,400334);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(76,4,4,202404,199721);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(77,5,1,202404,43758);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(78,5,2,202404,235874);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(79,5,3,202404,224269);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(80,5,4,202404,63588);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(81,1,1,202405,25199);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(82,1,2,202405,34538);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(83,1,3,202405,343718);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(84,1,4,202405,176656);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(85,2,1,202405,264023);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(86,2,2,202405,268814);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(87,2,3,202405,275766);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(88,2,4,202405,104226);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(89,3,1,202405,127990);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(90,3,2,202405,116280);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(91,3,3,202405,165533);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(92,3,4,202405,18549);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(93,4,1,202405,320624);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(94,4,2,202405,114944);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(95,4,3,202405,100454);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(96,4,4,202405,288648);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(97,5,1,202405,25805);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(98,5,2,202405,60557);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(99,5,3,202405,91417);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(100,5,4,202405,252524);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(101,1,1,202406,66839);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(102,1,2,202406,63863);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(103,1,3,202406,30736);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(104,1,4,202406,24300);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(105,2,1,202406,135711);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(106,2,2,202406,572334);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(107,2,3,202406,35079);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(108,2,4,202406,136708);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(109,3,1,202406,254618);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(110,3,2,202406,31144);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(111,3,3,202406,125499);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(112,3,4,202406,223842);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(113,4,1,202406,44533);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(114,4,2,202406,68948);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(115,4,3,202406,179067);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(116,4,4,202406,130514);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(117,5,1,202406,92616);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(118,5,2,202406,182021);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(119,5,3,202406,64297);
insert into payments (pmnt_id, client_id, service_id, period, amount) values(120,5,4,202406,424842);

insert into charges (chg_id, client_id, service_id, period, amount) values(1,1,1,202401,196844);
insert into charges (chg_id, client_id, service_id, period, amount) values(2,1,2,202401,267631);
insert into charges (chg_id, client_id, service_id, period, amount) values(3,1,3,202401,252111);
insert into charges (chg_id, client_id, service_id, period, amount) values(4,1,4,202401,274700);
insert into charges (chg_id, client_id, service_id, period, amount) values(5,2,1,202401,291387);
insert into charges (chg_id, client_id, service_id, period, amount) values(6,2,2,202401,60855);
insert into charges (chg_id, client_id, service_id, period, amount) values(7,2,3,202401,251687);
insert into charges (chg_id, client_id, service_id, period, amount) values(8,2,4,202401,234442);
insert into charges (chg_id, client_id, service_id, period, amount) values(9,3,1,202401,254048);
insert into charges (chg_id, client_id, service_id, period, amount) values(10,3,2,202401,98551);
insert into charges (chg_id, client_id, service_id, period, amount) values(11,3,3,202401,285330);
insert into charges (chg_id, client_id, service_id, period, amount) values(12,3,4,202401,76600);
insert into charges (chg_id, client_id, service_id, period, amount) values(13,4,1,202401,194238);
insert into charges (chg_id, client_id, service_id, period, amount) values(14,4,2,202401,51815);
insert into charges (chg_id, client_id, service_id, period, amount) values(15,4,3,202401,102817);
insert into charges (chg_id, client_id, service_id, period, amount) values(16,4,4,202401,211553);
insert into charges (chg_id, client_id, service_id, period, amount) values(17,5,1,202401,279095);
insert into charges (chg_id, client_id, service_id, period, amount) values(18,5,2,202401,146172);
insert into charges (chg_id, client_id, service_id, period, amount) values(19,5,3,202401,226530);
insert into charges (chg_id, client_id, service_id, period, amount) values(20,5,4,202401,119883);
insert into charges (chg_id, client_id, service_id, period, amount) values(21,1,1,202402,179165);
insert into charges (chg_id, client_id, service_id, period, amount) values(22,1,2,202402,215382);
insert into charges (chg_id, client_id, service_id, period, amount) values(23,1,3,202402,142452);
insert into charges (chg_id, client_id, service_id, period, amount) values(24,1,4,202402,105799);
insert into charges (chg_id, client_id, service_id, period, amount) values(25,2,1,202402,196605);
insert into charges (chg_id, client_id, service_id, period, amount) values(26,2,2,202402,156507);
insert into charges (chg_id, client_id, service_id, period, amount) values(27,2,3,202402,157640);
insert into charges (chg_id, client_id, service_id, period, amount) values(28,2,4,202402,63298);
insert into charges (chg_id, client_id, service_id, period, amount) values(29,3,1,202402,80795);
insert into charges (chg_id, client_id, service_id, period, amount) values(30,3,2,202402,17956);
insert into charges (chg_id, client_id, service_id, period, amount) values(31,3,3,202402,115802);
insert into charges (chg_id, client_id, service_id, period, amount) values(32,3,4,202402,231478);
insert into charges (chg_id, client_id, service_id, period, amount) values(33,4,1,202402,232677);
insert into charges (chg_id, client_id, service_id, period, amount) values(34,4,2,202402,286915);
insert into charges (chg_id, client_id, service_id, period, amount) values(35,4,3,202402,254717);
insert into charges (chg_id, client_id, service_id, period, amount) values(36,4,4,202402,118140);
insert into charges (chg_id, client_id, service_id, period, amount) values(37,5,1,202402,47384);
insert into charges (chg_id, client_id, service_id, period, amount) values(38,5,2,202402,187564);
insert into charges (chg_id, client_id, service_id, period, amount) values(39,5,3,202402,99998);
insert into charges (chg_id, client_id, service_id, period, amount) values(40,5,4,202402,191467);
insert into charges (chg_id, client_id, service_id, period, amount) values(41,1,1,202403,153511);
insert into charges (chg_id, client_id, service_id, period, amount) values(42,1,2,202403,281807);
insert into charges (chg_id, client_id, service_id, period, amount) values(43,1,3,202403,154496);
insert into charges (chg_id, client_id, service_id, period, amount) values(44,1,4,202403,160451);
insert into charges (chg_id, client_id, service_id, period, amount) values(45,2,1,202403,48359);
insert into charges (chg_id, client_id, service_id, period, amount) values(46,2,2,202403,171865);
insert into charges (chg_id, client_id, service_id, period, amount) values(47,2,3,202403,275515);
insert into charges (chg_id, client_id, service_id, period, amount) values(48,2,4,202403,41773);
insert into charges (chg_id, client_id, service_id, period, amount) values(49,3,1,202403,45739);
insert into charges (chg_id, client_id, service_id, period, amount) values(50,3,2,202403,34592);
insert into charges (chg_id, client_id, service_id, period, amount) values(51,3,3,202403,68541);
insert into charges (chg_id, client_id, service_id, period, amount) values(52,3,4,202403,192217);
insert into charges (chg_id, client_id, service_id, period, amount) values(53,4,1,202403,61585);
insert into charges (chg_id, client_id, service_id, period, amount) values(54,4,2,202403,12325);
insert into charges (chg_id, client_id, service_id, period, amount) values(55,4,3,202403,129619);
insert into charges (chg_id, client_id, service_id, period, amount) values(56,4,4,202403,204454);
insert into charges (chg_id, client_id, service_id, period, amount) values(57,5,1,202403,79926);
insert into charges (chg_id, client_id, service_id, period, amount) values(58,5,2,202403,269231);
insert into charges (chg_id, client_id, service_id, period, amount) values(59,5,3,202403,244556);
insert into charges (chg_id, client_id, service_id, period, amount) values(60,5,4,202403,103938);
insert into charges (chg_id, client_id, service_id, period, amount) values(61,1,1,202404,240848);
insert into charges (chg_id, client_id, service_id, period, amount) values(62,1,2,202404,129809);
insert into charges (chg_id, client_id, service_id, period, amount) values(63,1,3,202404,130954);
insert into charges (chg_id, client_id, service_id, period, amount) values(64,1,4,202404,232780);
insert into charges (chg_id, client_id, service_id, period, amount) values(65,2,1,202404,52639);
insert into charges (chg_id, client_id, service_id, period, amount) values(66,2,2,202404,200512);
insert into charges (chg_id, client_id, service_id, period, amount) values(67,2,3,202404,137766);
insert into charges (chg_id, client_id, service_id, period, amount) values(68,2,4,202404,115935);
insert into charges (chg_id, client_id, service_id, period, amount) values(69,3,1,202404,275643);
insert into charges (chg_id, client_id, service_id, period, amount) values(70,3,2,202404,201506);
insert into charges (chg_id, client_id, service_id, period, amount) values(71,3,3,202404,156903);
insert into charges (chg_id, client_id, service_id, period, amount) values(72,3,4,202404,176722);
insert into charges (chg_id, client_id, service_id, period, amount) values(73,4,1,202404,28983);
insert into charges (chg_id, client_id, service_id, period, amount) values(74,4,2,202404,34494);
insert into charges (chg_id, client_id, service_id, period, amount) values(75,4,3,202404,200167);
insert into charges (chg_id, client_id, service_id, period, amount) values(76,4,4,202404,199721);
insert into charges (chg_id, client_id, service_id, period, amount) values(77,5,1,202404,21879);
insert into charges (chg_id, client_id, service_id, period, amount) values(78,5,2,202404,235874);
insert into charges (chg_id, client_id, service_id, period, amount) values(79,5,3,202404,224269);
insert into charges (chg_id, client_id, service_id, period, amount) values(80,5,4,202404,31794);
insert into charges (chg_id, client_id, service_id, period, amount) values(81,1,1,202405,25199);
insert into charges (chg_id, client_id, service_id, period, amount) values(82,1,2,202405,69075);
insert into charges (chg_id, client_id, service_id, period, amount) values(83,1,3,202405,171859);
insert into charges (chg_id, client_id, service_id, period, amount) values(84,1,4,202405,176656);
insert into charges (chg_id, client_id, service_id, period, amount) values(85,2,1,202405,264023);
insert into charges (chg_id, client_id, service_id, period, amount) values(86,2,2,202405,268814);
insert into charges (chg_id, client_id, service_id, period, amount) values(87,2,3,202405,137883);
insert into charges (chg_id, client_id, service_id, period, amount) values(88,2,4,202405,104226);
insert into charges (chg_id, client_id, service_id, period, amount) values(89,3,1,202405,127990);
insert into charges (chg_id, client_id, service_id, period, amount) values(90,3,2,202405,116280);
insert into charges (chg_id, client_id, service_id, period, amount) values(91,3,3,202405,165533);
insert into charges (chg_id, client_id, service_id, period, amount) values(92,3,4,202405,18549);
insert into charges (chg_id, client_id, service_id, period, amount) values(93,4,1,202405,160312);
insert into charges (chg_id, client_id, service_id, period, amount) values(94,4,2,202405,229888);
insert into charges (chg_id, client_id, service_id, period, amount) values(95,4,3,202405,100454);
insert into charges (chg_id, client_id, service_id, period, amount) values(96,4,4,202405,144324);
insert into charges (chg_id, client_id, service_id, period, amount) values(97,5,1,202405,25805);
insert into charges (chg_id, client_id, service_id, period, amount) values(98,5,2,202405,60557);
insert into charges (chg_id, client_id, service_id, period, amount) values(99,5,3,202405,182833);
insert into charges (chg_id, client_id, service_id, period, amount) values(100,5,4,202405,252524);
insert into charges (chg_id, client_id, service_id, period, amount) values(101,1,1,202406,133678);
insert into charges (chg_id, client_id, service_id, period, amount) values(102,1,2,202406,127726);
insert into charges (chg_id, client_id, service_id, period, amount) values(103,1,3,202406,30736);
insert into charges (chg_id, client_id, service_id, period, amount) values(104,1,4,202406,48600);
insert into charges (chg_id, client_id, service_id, period, amount) values(105,2,1,202406,271421);
insert into charges (chg_id, client_id, service_id, period, amount) values(106,2,2,202406,286167);
insert into charges (chg_id, client_id, service_id, period, amount) values(107,2,3,202406,35079);
insert into charges (chg_id, client_id, service_id, period, amount) values(108,2,4,202406,273416);
insert into charges (chg_id, client_id, service_id, period, amount) values(109,3,1,202406,254618);
insert into charges (chg_id, client_id, service_id, period, amount) values(110,3,2,202406,31144);
insert into charges (chg_id, client_id, service_id, period, amount) values(111,3,3,202406,125499);
insert into charges (chg_id, client_id, service_id, period, amount) values(112,3,4,202406,223842);
insert into charges (chg_id, client_id, service_id, period, amount) values(113,4,1,202406,89065);
insert into charges (chg_id, client_id, service_id, period, amount) values(114,4,2,202406,68948);
insert into charges (chg_id, client_id, service_id, period, amount) values(115,4,3,202406,179067);
insert into charges (chg_id, client_id, service_id, period, amount) values(116,4,4,202406,130514);
insert into charges (chg_id, client_id, service_id, period, amount) values(117,5,1,202406,185231);
insert into charges (chg_id, client_id, service_id, period, amount) values(118,5,2,202406,182021);
insert into charges (chg_id, client_id, service_id, period, amount) values(119,5,3,202406,64297);
insert into charges (chg_id, client_id, service_id, period, amount) values(120,5,4,202406,212421);

commit;
```

## PIVOT in Oracle

### Example 1

```sql
select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id;

select lastname, Electric_sum/100, Gas_sum/100, ColdWater_sum/100, HotWater_sum/100 from (
select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id) 
PIVOT (sum(amount) sum for serv in (1 as Electric, 2 as Gas, 3 as ColdWater, 4 as HotWater));
--в названии столбца сверху добавляется суффикс из _ и алиаса аггрегирующего столбца
```

### Example 2

```sql
select clients.lastname as lastname, payments.service_id as serv, payments.amount as pmnt_amount, charges.amount chg_amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id
inner join scott.charges on clients.client_id=charges.client_id 
and payments.period=charges.period;

select lastname, Electric_pmntsum/100, Gas_pmntsum/100, ColdWater_pmntsum/100, HotWater_pmntsum/100,
Electric_chgsum/100, Gas_chgsum/100, ColdWater_chgsum/100, HotWater_chgsum/100 from (
select clients.lastname as lastname, payments.service_id as serv, payments.amount as pmnt_amount, charges.amount chg_amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id
inner join scott.charges on clients.client_id=charges.client_id 
and payments.period=charges.period)
PIVOT (sum(pmnt_amount) pmntsum, sum(chg_amount) chgsum  for serv in (1 as Electric, 2 as Gas, 3 as ColdWater, 4 as HotWater))
;
```

## CASE in Oracle

```sql
select lastname,
    sum(case when serv = 1 then amount else 0 end)/100 as Electic_sum,
    sum(case when serv = 2 then amount else 0 end)/100 as Gas_sum,
    sum(case when serv = 3 then amount else 0 end)/100 as ColdWater_sum,
    sum(case when serv = 4 then amount else 0 end)/100 as HotWater_sum
from 
(select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id)
group by lastname;
```

## CASE in PostgreSQL

```sql
select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from clients inner join payments on clients.client_id=payments.client_id;


select lastname,
    sum(case when serv = 1 then amount else 0 end)/100 as Electic_sum,
    sum(case when serv = 2 then amount else 0 end)/100 as Gas_sum,
    sum(case when serv = 3 then amount else 0 end)/100 as ColdWater_sum,
    sum(case when serv = 4 then amount else 0 end)/100 as HotWater_sum
from 
(select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from clients inner join payments on clients.client_id=payments.client_id) as t
group by lastname;
```
PS: В отличии от Oracle в PosgreSQL необходимо указать алиас вложенного запроса.

## Load example data for UNPIVOT

### Load in Oracle DB

```sql
create table scott.favorite_cities (client_name varchar2(100) not null, city_1 varchar2(100), city_2 varchar2(100), city_3 varchar2(100));
insert into scott.favorite_cities values ('Савельев','Москва','Сочи','Санкт-Петербург');
insert into scott.favorite_cities values ('Ветров','Омск','Новосибирск','Иркутск');
insert into scott.favorite_cities values ('Липатов','Санкт-Петербург','Иркутск','Сочи');
insert into scott.favorite_cities values ('Астафьев','Сочи','Новосибирск','Москва');
commit;
```

### Load in PostgreSQL

```sql
create table favorite_cities (client_name varchar(100) not null, city_1 varchar(100), city_2 varchar(100), city_3 varchar(100));
insert into favorite_cities values ('Савельев','Москва','Сочи','Санкт-Петербург');
insert into favorite_cities values ('Ветров','Омск','Новосибирск','Иркутск');
insert into favorite_cities values ('Липатов','Санкт-Петербург','Иркутск','Сочи');
insert into favorite_cities values ('Астафьев','Сочи','Новосибирск','Москва');
```

## UNPIVOT Oracle

```sql
select * from scott.favorite_cities;

select client_name, city, rank from scott.favorite_cities
UNPIVOT
(city for rank in (city_1 as 1, city_2 as 2, city_3 as 3));
```

## UNION ALL Oracle

```sql
with all_cities as 
(select client_name, city_1 as city, 1 as rank from scott.favorite_cities
 union all
 select client_name, city_2 as city, 2 as rank from scott.favorite_cities
 union all
 select client_name, city_3 as city, 3 as rank from scott.favorite_cities)
select * from all_cities order by client_name, rank;
```

## UNION ALL PostgreSQL

```sql
with all_cities as 
(select client_name, city_1 as city, 1 as rank from favorite_cities
 union all
 select client_name, city_2 as city, 2 as rank from favorite_cities
 union all
 select client_name, city_3 as city, 3 as rank from favorite_cities)
select * from all_cities order by client_name, rank;
commit;
```

## Настройки sqlplus для красивого вывода

```sql
SET PAGESIZE 1000
SET LINESIZE 200
col lastname format a10
col client_name format a15
col city format a15
col city_1 format a15
col city_2 format a15
col city_3 format a15
```


### Plans 

#### Plan for PIVOT Oracle

```sql
explain plan for 
select lastname, Electric_sum/100, Gas_sum/100, ColdWater_sum/100, HotWater_sum/100 from (
select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id) 
PIVOT (sum(amount) sum for serv in (1 as Electric, 2 as Gas, 3 as ColdWater, 4 as HotWater));

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY(format => 'ALL'));
 
Plan hash value: 375224469
 
-----------------------------------------------------------------------------------------------
| Id  | Operation                     | Name          | Rows  | Bytes | Cost (%CPU)| Time     |
-----------------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT              |               |       |       |     7 (100)|          |
|   1 |  HASH GROUP BY PIVOT          |               |     5 |   145 |     7  (29)| 00:00:01 |
|   2 |   MERGE JOIN                  |               |   120 |  3480 |     6  (17)| 00:00:01 |
|   3 |    TABLE ACCESS BY INDEX ROWID| PAYMENTS      |   120 |  1320 |     2   (0)| 00:00:01 |
|   4 |     INDEX FULL SCAN           | PAYMENTS_CLID |   120 |       |     1   (0)| 00:00:01 |
|*  5 |    SORT JOIN                  |               |     5 |    90 |     4  (25)| 00:00:01 |
|   6 |     TABLE ACCESS FULL         | CLIENTS       |     5 |    90 |     3   (0)| 00:00:01 |
-----------------------------------------------------------------------------------------------
```

#### Plan for CASE Oracle

```sql
explain plan for 
select lastname,
    sum(case when serv = 1 then amount else 0 end)/100 as Electic_sum,
    sum(case when serv = 2 then amount else 0 end)/100 as Gas_sum,
    sum(case when serv = 3 then amount else 0 end)/100 as ColdWater_sum,
    sum(case when serv = 4 then amount else 0 end)/100 as HotWater_sum
from 
(select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id)
group by lastname;

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY(format => 'ALL'));

Plan hash value: 1455264812
 
----------------------------------------------------------------------------------------------------------
| Id  | Operation                                | Name          | Rows  | Bytes | Cost (%CPU)| Time     |
----------------------------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT                         |               |       |       |     6 (100)|          |
|   1 |  HASH GROUP BY                           |               |     5 |   365 |     6  (34)| 00:00:01 |
|   2 |   MERGE JOIN                             |               |     5 |   365 |     5  (20)| 00:00:01 |
|   3 |    TABLE ACCESS BY INDEX ROWID           | CLIENTS       |     5 |    90 |     2   (0)| 00:00:01 |
|   4 |     INDEX FULL SCAN                      | SYS_C006863   |     5 |       |     1   (0)| 00:00:01 |
|*  5 |    SORT JOIN                             |               |     5 |   275 |     3  (34)| 00:00:01 |
|   6 |     VIEW                                 | VW_GBC_5      |     5 |   275 |     2   (0)| 00:00:01 |
|   7 |      HASH GROUP BY                       |               |     5 |    55 |     2   (0)| 00:00:01 |
|   8 |       TABLE ACCESS BY INDEX ROWID BATCHED| PAYMENTS      |   120 |  1320 |     2   (0)| 00:00:01 |
|   9 |        INDEX FULL SCAN                   | PAYMENTS_CLID |   120 |       |     1   (0)| 00:00:01 |
----------------------------------------------------------------------------------------------------------
```

#### Plans CASE PostgreSQL

```sql
explain
select lastname,
    sum(case when serv = 1 then amount else 0 end)/100 as Electic_sum,
    sum(case when serv = 2 then amount else 0 end)/100 as Gas_sum,
    sum(case when serv = 3 then amount else 0 end)/100 as ColdWater_sum,
    sum(case when serv = 4 then amount else 0 end)/100 as HotWater_sum
from 
(select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from clients inner join payments on clients.client_id=payments.client_id) as t
group by lastname;

HashAggregate  (cost=19.05..21.45 rows=120 width=250)
  Group Key: clients.lastname
  ->  Hash Join  (cost=13.82..16.35 rows=120 width=224)
        Hash Cond: (payments.client_id = clients.client_id)
        ->  Seq Scan on payments  (cost=0.00..2.20 rows=120 width=8)
        ->  Hash  (cost=11.70..11.70 rows=170 width=220)
              ->  Seq Scan on clients  (cost=0.00..11.70 rows=170 width=220)
```

#### Plan for UNPIVOT Oracle

```sql
explain plan for 
select client_name, city, rank from scott.favorite_cities
UNPIVOT
(city for rank in (city_1 as 1, city_2 as 2, city_3 as 3));

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY(format => 'ALL'));

Plan hash value: 638632602
 
---------------------------------------------------------------------------------------
| Id  | Operation           | Name            | Rows  | Bytes | Cost (%CPU)| Time     |
---------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT    |                 |    12 |  1284 |     5   (0)| 00:00:01 |
|*  1 |  VIEW               |                 |    12 |  1284 |     5   (0)| 00:00:01 |
|   2 |   UNPIVOT           |                 |       |       |            |          |
|   3 |    TABLE ACCESS FULL| FAVORITE_CITIES |     4 |   264 |     3   (0)| 00:00:01 |
---------------------------------------------------------------------------------------
```

#### Plan for UNION Oracle

```sql
```

#### Plan for UNION PostgreSQL

```sql
```



