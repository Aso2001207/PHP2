```uml
@startuml

!define MASTER_MARK_COLOR Orange
!define TEBUE_MARK_COLOR RED
!define TRANSACTION_MARK_COLOR DeepSkyBlue

'グラデーションさせる場合 #xx-xx
!define MAIN_ENTITY #MintCream-MistyRose

/'
  デフォルト色を"skinparam class"で設定します。
'/
skinparam class {
    '図の背景
    BackgroundColor Snow
    '図の枠
    BorderColor Black
    'リレーションの色
    ArrowColor Black
}

package "アテンダントマネジメントシステム" as target_system {


 entity "就業履歴テーブル" as d_work_history <d_work_history> <<T,TEBUE_MARK_COLOR>>{
+ history_code[PK][NN]
--
user_id
name
date
day_of_week
work_code
re_st_time
re_en_time
br_st
br_en
re_work_time
abs_flg
night_flg
del_flg

}


entity "シフトテーブル" as d_shift <d_shift> <<T,TEBUE_MARK_COLOR>>{
+ shift_code[PK][NN]
--
user_code
name
date
day_of_week
work_code
st_time
en_time
work_time
br_code
night_flg
del_flg


}



entity "個人情報マスタ" as m_personal_info <m_personal_info> <<M,MASTER_MARK_COLOR>>{
+ user_code [PK][NN]
--
name
pass
mail
address
tel
hire_date
work_date
work_month
del_flg

}


entity "管理者" as m_Administrator <m_Administrator> <<M,MASTER_MARK_COLOR>>{
+ user_code[PK][NN]
--
name
pass
mail
address
tel
del_flg

}

entity "休憩マスタ" as m_break_time <m_break_time> <<M,MASTER_MARK_COLOR>>{
+ br_code[PK][NN]
+ 
--
work_divi
br_time

}




entity "作業マスタ" as m_work <m_work><<M,MASTER_MARK_COLOR>>{
+ work_code[PK][NN]
--
work_name
work_con

}
entity "給料マスタ" as m_salary <m_salary><<M,MASTER_MARK_COLOR>>{
+ sal_code[PK][NN]
--
work_code
time_code
hour_wage
divi_sal
}

entity "作業時間範囲マスタ" as m_working_time_range <m_working_time_range><<M,MASTER_MARK_COLOR>>{
+ time_code[PK][NN]
--
time_ran

}

m_personal_info ---ri-o{ d_work_history
m_personal_info -do-|{ d_shift
m_personal_info ||-le-|| m_Administrator
m_personal_info }|---- m_work
d_shift ||--|| m_Administrator
d_shift ---le-|{ m_break_time
d_shift }|-ri--- m_work
d_shift ||----|| d_work_history
d_shift }|-do--- m_working_time_range
m_work ---ri-|{ m_salary
m_salary }|---- m_working_time_range








@enduml
```






