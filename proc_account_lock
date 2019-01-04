DROP PROCEDURE IF EXISTS proc_account_lock()

DELIMITER //

CREATE PROCEDURE proc_account_lock()

BEGIN

DECLARE v_set_cnt int;



# 제한 수 지정

set v_set_cnt = 5;



# 계정 확인 및 잠금 설정

UPDATE mysql.user x

    inner join (

                    select

                        substring_index(replace(USERHOST,"'",''),'@',1) as acc,

                        substring_index(replace(USERHOST,"'",''),'@',-1) as acc_host

                    from information_schema.CONNECTION_CONTROL_FAILED_LOGIN_ATTEMPTS

                    where FAILED_ATTEMPTS >= v_set_cnt

                     ) y on x.user = y.acc and x.host = y.acc_host

set x.account_locked = 'Y';



# 계정 잠금 적용

set @locked_accept = 'flush privileges';

prepare stmt from @locked_accept;

execute stmt;

deallocate prepare stmt;



END //

DELIMITER ;
