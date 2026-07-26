void timer_cb(){
    send_data(pack_data<BnoReading>(bnoreading, BNOREADING));
}

BlitzTimer t1(timer_cb, 100);

jus pack and send lil bro